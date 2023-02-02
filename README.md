# How-remove-words-from-text-using-Python
how we remove qa-, dev-, etc from beanstalk service names



import re
file = open('/Users/saqib/Desktop/bitbucket-python/temp_rename/file.txt', 'r') 
lines = file.readlines()

def env_name_to_service_name(env):
    service_name = env.lower().replace("qa-", "")
    service_name = service_name.replace("-qa", "")
    service_name = service_name.lower().replace("dev-", "")
    service_name = service_name.replace("-dev", "")
    service_name = service_name.replace("green-", "")
    service_name = service_name.replace("-green", "")
    service_name = service_name.replace("blue-", "")
    service_name = service_name.replace("-blue", "")
    service_name = re.sub(r"rg0[1-3]\-", "", service_name)
    service_name = re.sub(r"\-?p[0-9]\-?", "", service_name)
    service_name = re.sub(r"\-[0-9]$", "", service_name)
    
    return service_name

service_list = []
for line in lines:
    env_name = line.strip('\n')
    service_list.append(env_name_to_service_name(env_name))

final_service_list = list(set(service_list))
for service in final_service_list:
    print(service)
