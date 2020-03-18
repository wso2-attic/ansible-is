# Continuous Update Delivery for WSO2 Identity Server

### Prequisites
* Product packs should be provided in the `/files/packs` directory

### Usage
While executing the update script, provide the profile name. The pack corresponding to the profile will begin updating.
```bash
./update.sh -p <profile-name>
```
Any of the following profile names can be provided as arguments:
* is

example:
```bash
./update.sh -p is
```

If any file that is used as a template is updated, a warning will be displayed. Update the relevant template files accordingly before pushing updates to the nodes.
