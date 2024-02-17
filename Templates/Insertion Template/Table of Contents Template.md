
<%*
// Will update this in future
// Constants for TOC markers
const markerTOCstart = '>[!SUMMARY]+ Table of Contents';
const markerTOCend = '%%ENDTOC%%';

// Get the active file and its metadata
const activeFile = await this.app.workspace.getActiveFile();
const mdCache = await this.app.metadataCache.getFileCache(activeFile);

// Get the current file content and split it into lines
const fileContent = await tp.file.content;
const fileContentSplit = fileContent.split('\n');

// Check if the file starts with a YAML frontmatter block
let hasYAML = fileContentSplit[0] === '---' && fileContentSplit.indexOf('---', 1) > 0;
let yamlEndLine = hasYAML ? fileContentSplit.indexOf('---', 1) : -1;

// Find existing TOC start and end positions
let TOCstart = fileContentSplit.indexOf(markerTOCstart);
let TOCend = fileContentSplit.indexOf(markerTOCend, TOCstart);

// Remove existing TOC if it exists
if (TOCstart !== -1 && TOCend !== -1) {
fileContentSplit.splice(TOCstart, TOCend - TOCstart + 1);
}

// Initialize an empty array to hold new TOC lines
let newTOC = [];

// Get header limit from user
let header_limit = await tp.system.prompt("Show Contents Down to Which Header Level (1-6)?", "3");

const mdCacheListItems = mdCache.headings;
if (mdCacheListItems && mdCacheListItems.length > 0) {
// Generate new TOC
mdCacheListItems.forEach(item => {
var header_text = item.heading;
var header_level = item.level;

if (header_level <= header_limit) {
let file_title = tp.file.title.replace(/ /g, '%20');
let header_url = header_text.replace(/ /g, '%20');
let header_link = `[${header_text}](${file_title}.md#${header_url})`;
newTOC.push(`>${' '.repeat(header_level - 1) + '- ' + header_link}`);
}
});
}

// Determine where to insert the new TOC
let insertPosition = hasYAML ? yamlEndLine + 1 : 0;
if (TOCstart !== -1) insertPosition = TOCstart;

// Add or remove TOC based on newTOC's content
if (newTOC.length > 0) {
// Insert the new TOC into the file content
fileContentSplit.splice(insertPosition, 0, markerTOCstart, ...newTOC, "", markerTOCend);
} else if (TOCstart !== -1 && TOCend !== -1) {
// Remove the markers when there are no headers
fileContentSplit.splice(TOCstart, TOCend - TOCstart + 1);
}

// Update the file with the new content
await app.vault.modify(activeFile, fileContentSplit.join('\n'));
%>