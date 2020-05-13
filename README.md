# folding-at-home-pauser
I needed a way to pause folding at home when sharing video during zoom meetings because my video would lag.

You can obviously swap out "zoom" for any program that FAH causes issues for (webex, pugb, etc). You'll need to modify the memory # to your needs.

I'm sure there's a more elegant way to do this (feel free to share), but I couldn't find anything in all of the Internet, so sharing here for anyone else. Hope it saves you some time.

It checks to see how much private memory is being used by zoom. I found that the value below was a reliable indicator that my video was on. 


$command="C:\Program Files (x86)\FAHClient\FAHClient.exe" ; $x="zoom" |ForEach-Object{Get-Process -name $_ | Measure-Object PrivateMemorySize -sum | Select-Object @{Name="Name";Expression = {$pv.name}}, Sum}; echo $x.sum;if ($x.sum -gt 200000000){$arguments="--send-pause";echo "zoom running, pausing";Start-Process $command $arguments} else {$arguments="--send-unpause";echo "zoom not running, folding";;Start-Process $command $arguments}

Just have task scheduler run it every minute.
