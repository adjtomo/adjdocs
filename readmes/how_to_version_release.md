# adjTomo Package Version Release Checklist

Checklist for any version release relating to semantic version number
incrementation. Please include in any PR to master and make sure all points
are checked off when incrementing any of the version numbers (major, minor, 
patch), or provide reason in PR for why certain points are not checked.

## Prior to PR merge:
- [ ] Merge `devel` -> `master`
- [ ] Bump version number `pyproject.toml`
- [ ] Ensure all tests still pass, fix broken tests
- [ ] Update `CHANGELOG` to include all major changes since last version

## Following PR merge:
- [ ] Create GitHub version release
- [ ] Publish latest version on PyPi
- [ ] Post on adjTomo Discussion for major and minor version releases

## Publishing Package on PyPi
*Useful link: https://realpython.com/pypi-publish-python-package/*

1. Ensure your `pyproject.toml` file is set up properly; required fields are name and version
2. Set dependencies, do **not** pin exact versions but allow for upper and lower bounds; only list direct dependencies
3. Include `tests/`, `docs/`, license, and MANIFEST files (MANIFIST used for including non-source code material
4. Ensure you have an account on PyPi and TestPyPi (for testing publishing)
5. Install `twine` and `build` which are used to build and push packages to PyPi
6. Build your packages locally, which creates the `.tar.gz` and `.whl` dist files
```bash
python -m build
```
6. Check that files in your .whl (zip file) are as expected (including everything in 3)
7. Check dist files with:
```bash
twine check dist/*
```
8. Upload test package (note: requires TestPyPi account)
```bash
twine upload -r testpypi dist/*
```
9. Upload real package (note: requires PyPi account)
```bash
twine upload dist/*
```
