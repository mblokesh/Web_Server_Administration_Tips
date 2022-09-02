```
<?php
$output = shell_exec('hostname -I');
echo "Your IP address is:";
echo $output;
?>
```