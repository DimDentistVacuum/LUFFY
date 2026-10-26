import urllib.request, base64, json
token = open('/workspace/dumps/workspace/.github_token').read().strip()
content = open('/workspace/dumps/workspace/repo/README_new.md','rb').read()
payload = json.dumps({
    'message': 'docs: update Complete TODO List after implementing items in deepscaler utils and protocol',
    'content': base64.b64encode(content).decode(),
    'sha': 'ede832d1fcdfa1344615873c29eaccfbe3f99e96',
    'branch': 'dev'
}).encode()
req = urllib.request.Request(
    'https://api.github.com/repos/DimDentistVacuum/LUFFY/contents/README.md',
    data=payload, method='PUT',
    headers={'Authorization': f'token {token}', 'User-Agent':'agent',
             'Accept':'application/vnd.github+json', 'Content-Type':'application/json'})
resp = json.loads(urllib.request.urlopen(req).read())
print(resp['commit']['sha'])
print(resp['content']['sha'])
