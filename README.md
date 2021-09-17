# GitHub Action to Setup The Poetry Environment

This action can be used to set up the Poetry Environment. The action tries to load the environment from the cache. If the cache does not exist, the fresh environment is installed and saved to the cache.

The following key syntax is used to check if the cache exists:
```
key: "${{ runner.os }}-poetry-${{ steps.python-setup.outputs.python-version }}-${{ hashFiles('./poetry.lock') }}"
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

No variables

## Output variables

* `cache-used`: Returns `True` if the environment was loaded from the cache, or `False` if the fresh environment is installed.
