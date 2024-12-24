# EdgeGrid for cURL

This library implements an Authentication handler for HTTP requests using the [Akamai EdgeGrid Authentication](https://techdocs.akamai.com/developer/docs/authenticate-with-edgegrid) scheme for cURL.

`egcurl` is a simple Python-based command wrapper around the traditional [cURL](https://curl.se) command to sign requests for Akamai OPEN APIs. The script intercepts a subset of cURL command arguments to produce a request signature. Then it uses cURL to make the API call with all the original arguments and the computed request signature.

> **Note:** There is now a simpler command line tool available, httpie. You don't need to be familiar with cURL to use httpie. It's available on the [httpie-edgegrid](https://github.com/akamai-open/httpie-edgegrid) GitHub repository.
>
> The examples and guides on the [developer portal](https://techdocs.akamai.com/home/page/apis) are moving to this new tool, thus consider using it for your API calls.

## Install

1. Install Python 3.6 or later on your system. You can download it from https://www.python.org/downloads/. If you're running GNU/Linux or macOS, you probably already have it.

   > __NOTE:__ Python 2 is no longer supported by the [Python Software Foundation](https://www.python.org/doc/sunset-python-2/). You won't be able to use the library with Python 2.

2. Install [cURL](https://curl.se/download.html). The script expects to find it in your path.

3. Install the `edgegrid-python` authentication handler to sign your requests by running this command:

   ```
   pip install edgegrid-python
    ```

4. Clone this repository: https://github.com/akamai/edgegrid-curl.git
and then execute `egcurl` directly from the cloned repository.

## Authentication

We provide authentication credentials through an API client. Requests to the API are signed with a timestamp and are executed immediately.

1. [Create authentication credentials](https://techdocs.akamai.com/developer/docs/set-up-authentication-credentials).

2. Place your credentials in an EdgeGrid resource file, `.edgerc`, under a heading of `[default]` at your local home directory or the home directory of a web-server user.

   ```
   [default]
    client_secret = C113nt53KR3TN6N90yVuAgICxIRwsObLi0E67/N8eRN=
    host = akab-h05tnam3wl42son7nktnlnnx-kbob3i3v.luna.akamaiapis.net
    access_token = akab-acc35t0k3nodujqunph3w7hzp7-gtm6ij
    client_token = akab-c113ntt0k3n4qtari252bfxxbsl-yvsdj
   ```

3. Use `egcurl` to sign your requests along with and `--eg-edgerc` argument to point to the path of your `.edgerc` configuration file and an `--eg-section` argument to specify the credentials' section header.

   ```shell
   python3 egcurl --eg-edgerc ~/.edgerc --eg-section default --request GET
   ```


## Use

To use the library, provide the credential's section header of your `.edgerc` file and the appropriate endpoint information.

```shell
python3 egcurl --eg-edgerc ~/.edgerc --eg-section default --request GET \
     --url "https://luna.akamaiapis.net/identity-management/v3/user-profile" \
     --header 'accept: application/json'
```
















