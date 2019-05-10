# Debugging Practices with DSB2018 tran.py and valid.py
## Issue with forking
As we described in README.md, VS Code debugger does not support `fork` in the meanwhile, hence the `multiprocessing.Manager()` and `DataLoader` from `torch.utils.data` will cause erros when debugging. I've tried changing the `fork` method to `spawn` by adding
```python
multiprocessing.set_start_method('spawn', force=True)
``` 
before using any `multiprocessing` components, but unfortunately that does not work for me. So one possible workarond is to disable multiprocessing when debugging, and make sure that everything else is working fine, then we can add them back when running.

So, you will need to disable the use of `Manager()` and set `cache` to `None`, since we're not using multiple workers while debugging, there's no need for the IPC manager.

Also, to disable `fork` in `DataLoader`, set `n_worker = 0` in `config.ini`.
