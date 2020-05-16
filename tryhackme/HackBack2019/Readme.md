# [Task 3] [Scripting] [Medium] Gotta Catch em All
```python
import requests
import re
import time
url = "http://10.10.207.179:"
first_port = 3010
result_number=0

response = requests.get(url+str(first_port))
cut_response = response.text[853:]
next_port = re.match(r"[0-9]+",cut_response).group(0)
print(response.text)
while True:
  next_url=url+next_port
  print(next_url)
  try:
    response = requests.get(next_url)
  except Exception :
    time.sleep(1)
    try:
      time.sleep(1)
      response = requests.get(next_url)
    except Exception:
      response = requests.get(next_url)
  operations = response.text.split(" ")

  if operations[0] =="STOP":
    print("STOP")
    break
  elif operations[0] == "add":
    result_number = result_number + int(operations[1])
  elif operations[0] == "minus":
    result_number = result_number - int(operations[1])
  elif operations[0] == "multiply":
    result_number = result_number * int(operations[1])
  elif operations[0] == "divide":
    result_number = result_number / int(operations[1])
  else:
    print(operations[0]) 
    break
  next_port = operations[2]
print("result_number:"+str(result_number))
 
```
