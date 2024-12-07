---
title: Downloads
url: downloads/index.php
---

<?php
$versions = [];
// We'll probably do this a better way later, but for now, every version contains a windows installer.
$files = glob("nvgt_*.exe");
foreach ($files as $file) {
	$ver = substr($file, 5, -4);
	if ($ver == "") continue;
	$versions[] = $ver;
}
rsort($versions);
// Function from https://stackoverflow.com/questions/15188033/human-readable-file-size
function size2string($bytes) {
	$i = floor(log($bytes) / log(1024));
	$sizes = array('B', 'KB', 'MB', 'GB', 'TB', 'PB', 'EB', 'ZB', 'YB');
	return sprintf('%.02F', $bytes / pow(1024, $i)) * 1 . ' ' . $sizes[$i];
}
// This function prints the information for a given version, again still a bit hacky.
function echo_version($ver) {
	echo "<h3>" . $ver . "</h3>\n";
	echo "<p>Released on <script>document.write(local_datetime_string(" . (filemtime("nvgt_" . $ver . ".exe") * 1000) . "));</script>.</p>\n";
	$files = glob("nvgt_" . $ver . "*");
	echo "<ul>\n";
	foreach($files as $file) {
		echo '<li><a href="' . $file . '">' .$file. '</a> (' . size2string(filesize($file)) . ')</li>';
	}
	echo "</ul>\n";
}
?>

<h1>Downloads</h1>
<p>This page contains the latest binary releases for NVGT for windows, Mac OS and Linux.</p>
<p>Please note that the stability of these packages is still actively improving as NVGT's first public release happened very recently.</p>
<p>Since several people have asked, yes we do soon intend to interface with github releases. I'm not sure we will entirely abandon the idea of this page, but either this page will link to release artifacts on Github, our github releases will link to this page, or both if needed.</p>

<?php
if (count($versions) < 1) {
	echo "<p>Oops, cannot find any files to list!</p>";
} else {
?>
<h2>latest version</h2>
<?php echo_version($versions[0]); ?>
<h2>older versions</h2>
<?php
echo "<p>There are a total of " . count($versions) -1 . " older versions available for download.</p>\n";
$counter = 0;
while (++$counter < count($versions)) echo_Version($versions[$counter]);

} // end no files check above
?>
