## 4.0.0

- Forked from basicScroll.
- Added jQuery wrapper `hScroll`.
- Added auto detection on `data-timing` attribute.
- Changed the format of `props` argument: Variable can be put on 1st level, no longer needed to be children of "props".
- Added alternative way of specifying `props` arguments: Using data attribute with double dash like `data--opacity="0.2 to 1"`. It will update the variable `--opacity` from 0.2 to 1.

Default value for arguments:

- Added default value for argument **from**: "middle-bottom".
- Added default value for argument **to**: "middle-top".