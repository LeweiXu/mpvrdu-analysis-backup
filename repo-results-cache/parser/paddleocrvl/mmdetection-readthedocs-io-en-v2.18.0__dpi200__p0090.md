pass
def before_run(self, runner):
    pass
def after_run(self, runner):
    pass
def before_epoch(self, runner):
    pass
def after_epoch(self, runner):
    pass
def before_iter(self, runner):
    pass
def after_iter(self, runner):
    pass

(continued from previous page)

Depending on the functionality of the hook, the users need to specify what the hook will do at each stage of the training in before_run, after_run, before_epoch, after_epoch, before_iter, and after_iter.

### 2. Register the new hook

Then we need to make MyHook imported. Assuming the file is in mmdet/core/utils/my_hook.py there are two ways to do that:

• Modify mmdet/core/utils/__init__.py to import it.

The newly defined module should be imported in mmdet/core/utils/__init__.py so that the registry will find the new module and add it:

from.my_hook import MyHook

• Use custom_imports in the config to manually import it

custom_imports = dict(imports=['mmdet.core.utils.my_hook'], allow_failed_imports=False)

### 3. Modify the config

custom_hooks = [
dict(type='MyHook', a=a_value, b=b_value)]

You can also set the priority of the hook by adding key priority to 'NORMAL' or 'HIGHEST' as below.

custom_hooks = [
dict(type='MyHook', a=a_value, b=b_value, priority='NORMAL')
]

By default the hook’s priority is set as NORMAL during registration.

#### 12.4. Customize hooks