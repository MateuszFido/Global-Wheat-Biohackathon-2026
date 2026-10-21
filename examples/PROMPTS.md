## PROMPTS.md

These two prompt examples showcase how agents can be used to create a small viewer application with a chosen tech stack.


### Python + Streamlit

Initial prompt:

```{text}
Create a working Streamlit app in app.py in the current directory.

Build a "Wheat Image Explorer" using streamlit, requests, and Pillow,
all of which are already installed.

Requirements:
- A dropdown selecting between these two public images:
  GWHD: https://data.global-wheat.com/gwhd/images/00000000.jpg
  GWFSS: https://data.global-wheat.com/gwfss/images/00000000.png
- Fetch images server-side with a request timeout and cache downloads.
- Display the selected image and its original pixel dimensions.
- Add a contrast slider that updates the displayed image, using Pillow.
- Add a button to download the original image.
- Show errors if downloading or decoding fails.

Do not read secrets, do not change environment files. Use only publicly available image URLs.
```

Then, start the server:

```{sh}
echo "The app preview is available at: ${RENKU_BASE_URL%/}/proxy/absolute/8501/"

python -m streamlit run app.py \
  --server.address=127.0.0.1 \
  --server.port=8501 \
  --server.headless=true \
  --server.runOnSave=true \
  --server.baseUrlPath="${RENKU_BASE_URL_PATH%/}/proxy/absolute/8501" \
  --browser.serverAddress="$(python -c 'import os; from urllib.parse import urlsplit; print(urlsplit(os.environ["RENKU_BASE_URL"]).hostname)')" \
  --browser.serverPort=443
```

You can then open the printed URL in another tab of your browser (outside of Renku).

Stop the server with Ctrl+C from the Renku terminal.

### TypeScript + Express

Prompt: 


```{text}
Create a working "Wheat Image Explorer" in a new typescript-app directory.

Use Node.js, TypeScript, Express, and plain browser JavaScript.
Use npm, install the required dependencies, and create package-lock.json.
Provide an "npm run dev" command using tsx watch.

Requirements:
- A dropdown selecting between these two public images:
  GWHD: https://data.global-wheat.com/gwhd/images/00000000.jpg
  GWFSS: https://data.global-wheat.com/gwfss/images/00000000.png
- Fetch the images server-side using Node's fetch, with a timeout.
- Map the two dataset IDs to those fixed URLs and cache downloads in memory.
- Serve the image bytes through the app's own backend.
- Display the selected image and its original pixel dimensions.
- Add a contrast slider using a browser canvas.
- Add a button to download the original image.
- Show useful errors if downloading or decoding fails.

Do not read secrets, do not change environment files. Use only publicly available image URLs.
```