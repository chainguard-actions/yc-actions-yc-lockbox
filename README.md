## GitHub Action to fetch secret from Yandex Cloud Lockbox.

The action fetches secret from Yandex Cloud Lockbox.

**Table of Contents**

<!-- toc -->

- [Usage](#usage)
- [Permissions](#permissions)
- [License Summary](#license-summary)

<!-- tocstop -->

## Usage

```yaml
    - name: Fetch secret
      id: lockbox-secret
      uses: yc-actions/yc-lockbox@v1
      with:
        yc-sa-json-credentials: ${{ secrets.YC_SA_JSON_CREDENTIALS }}
        secret-id: e6q************
```
`yc-sa-json-credentials` should contain JSON with authorized key for Service Account. More info in [Yandex Cloud IAM documentation](https://cloud.yandex.ru/docs/container-registry/operations/authentication#sa-json).

See [action.yml](action.yml) for the full documentation for this action's inputs and outputs.

## Permissions

To perform this action, it is required that the service account on behalf of which we are acting has granted the `cdn.editor` role or greater.

## License Summary

This code is made available under the MIT license.

## Privacy

This Action contacts Chainguard's licensing server to verify authorization. Connection metadata (IP address, GitHub repository identifier, timestamp, and any metadata encoded in the auth token) is transmitted to Chainguard, Inc. even if authorization is denied in accordance with our [Privacy Notice](https://www.chainguard.dev/legal/privacy-notice)
