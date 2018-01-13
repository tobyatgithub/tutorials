# Common Problems

### Changing code in PySyft isn't reflected in Jupyter Notebook

If you make a change in PySyft, whether that is pulling new code or making local changes,
make sure you have
- rerun the install script
`python setup.py install`.
- restarted the kernel in notebook

If the above does not work, it is possible that `python` and `jupyter` are not bundled together.
A test for this is to run
```
which python
which jupyter
```

and they should be under the same path, e.g.
```
$ which python
/Users/you/anaconda3/bin/python

$ which jupyter
/Users/you/anaconda3/bin/jupyter
```
