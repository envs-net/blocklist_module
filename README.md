# envs - synapse blocklist tool
An collection of modules for Synapse to block temporary email addresses and block invite-spam.  
This Tool generates a module config file for synapse in `/etc/matrix-synapse/conf.d/modules.yaml`.

Please do not use the tool if you do not understand what it does.
Also make sure that all dependencies are installed and that you have looked at all files in the repo.

# Installation

clone the repo to `/opt`:  
`git clone https://github.com/envs-net/synapse_blocklist_module.git /opt/synapse_blocklist_module`

## dependencies

The Debian and Ubuntu packages install the Python virtual environment at `/opt/venvs/matrix-synapse`.  
to switch to this venv use `cd /opt/venvs/matrix-synapse && source bin/activate`, then use pip to install the module.

The Arch package uses the system-wide Python environment; just use the system-wide pip (`/usr/bin/pip`)

> **Note**
> Where your python environment is depends on your installation method. Visit [#synapse:matrix.org](https://matrix.to/#/#synapse:matrix.org) if you're not sure.

### synapse-simple-antispam

**This requires Synapse 1.61.0 or higher**  
see: [https://git.envs.net/envs/synapse-simple-antispam/src/branch/master/README.md](https://git.envs.net/envs/synapse-simple-antispam/src/branch/master/README.md) for details.

#### Installation

In your Synapse Python environment:
```bash
pip install git+https://git.thisisjoes.site/joe/synapse-simple-antispam
```

### mjolnir synapse_antispam

**This requires Synapse 1.53.0 or higher**  
see: [https://github.com/matrix-org/mjolnir/blob/main/docs/synapse_module.md](https://github.com/matrix-org/mjolnir/blob/main/docs/synapse_module.md) for details.

#### Installation

In your Synapse Python environment:
```bash
pip install -e "git+https://github.com/matrix-org/mjolnir.git#egg=mjolnir&subdirectory=synapse_antispam"
```

# Usage

1. ensure synapse load config's from the conf.d path.  
  see for example [/etc/systemd/system/matrix-synapse.service](https://git.envs.net/envs/matrix-conf/src/branch/master/etc/systemd/system/matrix-synapse.service#L15).

2. remove the modules part from your `homeserver.yaml`.

3. modify your additional `blocked_domains` and `allowed_domains` as needed.

4. generate your modules.yaml via:  
  `bash /opt/synapse_blocklist_module/generate_blocklist`

> **Note**
> Synapse will need to be restarted to apply the updates in your modules.yaml.
