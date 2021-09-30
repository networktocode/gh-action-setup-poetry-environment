# GitHub Action to Setup The Poetry Environment

This action can be used to set up the Poetry Environment. The action tries to load the environment from the cache. If the cache does not exist, the fresh environment is installed and saved to the cache.

The following key syntax is used to check if the cache exists:
```
key: "${{ runner.os }}-poetry-${{ steps.python-setup.outputs.python-version }}-${{ hashFiles('./poetry.lock') }}${{ inputs.cache-version }}"
```

* Typically, the value of the first variable is `Linux`
* The second variable contains the python version. The value `3.9.7` is the example that can be used.
* The last variable calculates the hash of the `poetry.lock` file. If the `poetry.lock` is updated, then the hash is different, which means that the key is different.

The following is the example of the key:
```
Linux-poetry-3.9.7-3c5d9aa2fd2aec48fd6a7de22cde35e3d3193e2141961270823edbdf12c104ed
```

If the key is changed, then this action invalidates the cache and creates a new environment. The new environment is then saved to the cache.

## Input variables

* `python-version`: Defines the python version which will be deployed on the system. Example values are: `3.6`, `3.7`, `3.8`, `3.9`. Defaults to `3.9`.
* `cache-version`: Can be used to specify the different version of the cache. This string is appended to the key. Defaults to empty string.
## Output variables

* `cache-used`: Returns `True` if the environment was loaded from the cache, or empty string if the fresh environment is installed.
* `python-version`: Returns the exact version installed. For example: `3.6.15`, `3.7.12`, `3.8.12`, `3.9.7`
