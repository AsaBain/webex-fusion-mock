# Webex Fusion Mock Endpoint

This project publishes a static JSON response through GitHub Pages so the Webex Contact Center HTTP Request activity can be tested independently of the Fusion server.

## What the endpoint does

- Accepts an HTTPS `GET` request.
- Returns HTTP `200` with the supplied Fusion-style JSON response.
- Ignores `customerNumber` and `locationNumber`, so every request returns the same test record.
- Uses only sample data and does not collect or store request data.

## Publish with GitHub Pages

1. Create a new **public** GitHub repository, for example `webex-fusion-mock`.
2. Upload everything from this project to the repository's `main` branch.
3. In the repository, open **Settings → Pages**.
4. Under **Build and deployment**, select **Deploy from a branch**.
5. Select branch **main**, folder **/docs**, and click **Save**.
6. Wait for GitHub to show the published site URL. Initial publishing can take a few minutes.

The site URL will follow this format:

```text
https://YOUR-USERNAME.github.io/YOUR-REPOSITORY/
```

## Endpoint URL

Use this URL after replacing the username and repository name:

```text
https://YOUR-USERNAME.github.io/YOUR-REPOSITORY/FusionServices/v3/Naviline/Utilities/AccountInfo/response.json?customerNumber=100001&locationNumber=1
```

The query values can be changed without changing the response:

```text
https://YOUR-USERNAME.github.io/YOUR-REPOSITORY/FusionServices/v3/Naviline/Utilities/AccountInfo/response.json?customerNumber=999999&locationNumber=25
```

## Test in Postman

1. Create a new request.
2. Select **GET**.
3. Paste the endpoint URL.
4. Do not add a request body or authentication.
5. Click **Send**.

Expected result:

- Status: `200 OK`
- Response header: `Content-Type: application/json`
- Body: the JSON stored in `docs/FusionServices/v3/Naviline/Utilities/AccountInfo/response.json`

## Important limitation

GitHub Pages cannot process a dynamic route such as:

```text
/AccountInfo/100001/1
```

For this static test, use the fixed `response.json` path and pass the customer and location values as query parameters. GitHub Pages ignores the query values and returns the same file.
