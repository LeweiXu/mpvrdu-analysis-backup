### 17.3 Usage of init_cfg

### 1. Initialize model by layer key

If we only define layer, it just initialize the layer in layer key.

NOTE: Value of layer key is the class name with attributes weights and bias of Pytorch, (so such as MultiheadAttention layer is not supported).

• Define layer key for initializing module with same configuration.

init_cfg = dict(type='Constant', layer=['Conv1d', 'Conv2d', 'Linear'], val=1)
# initialize whole module with same configuration

• Define layer key for initializing layer with different configurations.

init_cfg = [dict(type='Constant', layer='Conv1d', val=1), dict(type='Constant', layer='Conv2d', val=2), dict(type='Constant', layer='Linear', val=3)]
# nn.Conv1d will be initialized with dict(type='Constant', val=1)
# nn.Conv2d will be initialized with dict(type='Constant', val=2)
# nn.Linear will be initialized with dict(type='Constant', val=3)

1. Initialize model by override key

- When initializing some specific part with its attribute name, we can use override key, and the value in override will ignore the value in init_cfg.

# layers
# self.feat = nn.Conv1d(3, 1, 3)
# self.reg = nn.Conv2d(3, 3, 3)
# self.cls = nn.Linear(1, 2)

init_cfg = dict(type='Constant',
                     layer=['Conv1d', 'Conv2d'], val=1, bias=2,
                     override=dict(type='Constant', name='reg', val=3, bias=4))

# self.feat and self.cls will be initialized with dict(type='Constant', val=1, bias=2)

# The module called'reg' will be initialized with dict(type='Constant', val=3, bias=4)

• If layer is None in init_cfg, only sub-module with the name in override will be initialized, and type and other args in override can be omitted.

# layers
# self.feat = nn.Conv1d(3, 1, 3)
# self.reg = nn.Conv2d(3, 3, 3)
# self.cls = nn.Linear(1, 2)

init_cfg = dict(type='Constant', val=1, bias=2, override=dict(name='reg'))

# self.feat and self.cls will be initialized by Pytorch
# The module called'reg' will be initialized with dict(type='Constant', val=1, bias=2)

• If we don’t define layer key or override key, it will not initialize anything.

• Invalid usage