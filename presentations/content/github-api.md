---
layout: article
category: presentations
title: "March 27, 2013 talk on the GitHub API, by Christopher Swenson"
---

The following are my `sliderepl` slides.

<pre>
from sliderepl import Deck
Deck.run()

### slide::
# Let's start by loading some stuff we're going to need.
import requests
import json
import os
from pprint import pprint

### slide::
# This can be different if you use GH:E
gh = 'https://api.github.com/'
user = 'swenson'
pw = os.environ['GITHUB_PASS'].strip()
auth = (user, pw) # useful for requests

def get(url, *args, **kwargs):
  return requests.get(gh + url, *args, **kwargs)
def post(url, *args, **kwargs):
  return requests.post(gh + url, *args, **kwargs)


### slide::
# optional, get an OAuth token
data = { 'note': 'testing' }
resp = post('authorizations', auth=auth, data=json.dumps(data))
token = resp.json()['token']
token

### slide::
authheaders = { 'authorization': 'token ' + token }

### slide::
resp = get('users/swenson/orgs', headers=authheaders)
# pprint(resp.json())

### slide::
resp = get('repos/swenson/sort/issues', headers=authheaders)
# pprint(resp.json())

### slide::
resp = get('repos/swenson/sort/pulls', headers=authheaders)
# pprint(resp.json())

### slide::
resp = get('repos/swenson/sort/pulls/6/comments', headers=authheaders)
# pprint(resp.json())

### slide::
resp = get('repos/swenson/sort/issues/6/comments', headers=authheaders)
# pprint(resp.json())

### slide::

data = {
  'title': "Test issue",
  'body': "Test body"
}
resp = post('repos/swenson/testrepo/issues',
  data=json.dumps(data),
  auth=auth)
# pprint(resp.json())

### slide::

# Talk about some things you've done, @swenson
#
# Docbrown
# Docwho
# swiper scoring
# trac importing

### slide::

# This is the end -- the next slide deletes the authorization

### slide::
# cleanup
resp = get('authorizations', auth=auth)
for token in resp.json():
  if token['note'] == 'testing':
    print 'deleting ' + token['token'],
    deleted = requests.delete(token['url'], auth=auth)
    print deleted.ok


### slide:: end
</pre>
