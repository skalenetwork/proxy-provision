# SKALE Proxy Provision

[![Discord](https://img.shields.io/discord/534485763354787851.svg)](https://discord.gg/vvUtWJB)

A set of ansible playbooks to setup SKALE Proxy and Block explorer in the cloud

## 1. Installation

> Make sure that you have Python 3.7+ installed

1. Clone this repo
2. Create venv & install requrements:

```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt 
```

## 2. Setup

1. Create inventory for your network:

```bash
cp inventory-template inventory
```

2. Fill variables in `hosts` file - put IP and username of proxy and explorer instances. 

If you need only proxy - remove `[explorer]` section from `hosts` file.

3. Fill variables in `inventory` file:

```bash
[proxy:vars]
domain= # optional - proxy domain name (for automated SSL setup)

[explorer:vars]
domain= # optional - explorer domain name (for automated SSL setup)

[all:vars]

base_path= # home path on the machine(s) - e.g. /home/ubuntu
do_token= # optional - DigitalOcean token (for automated SSL setup)
email= # optional - SSL cert email (for automated SSL setup)

ansible_ssh_user='' # username on machine(s) - e.g. ubuntu
ansible_python_interpreter=/usr/bin/python3

proxy_domain='' # proxy domain name
explorer_domain='' # explorer domain name (optional for proxy-only setup)
chain_id='0x1' # Chain ID of the network where SM contracts are deployed - e.g. 0x1
network_name='mainnet' # SKALE Network name - e.g. mainnet / staging / etc
eth_endpoint='' # Ethereum Mainnet endpoint

main_website_url='https://skale.network/' # SKALE Website URL
docs_website_url='https://docs.skale.network/docs/' # SKALE Docs Website URL
networks='{}' # Legacy variable, keep as is
abis_url='https://github.com/skalenetwork/skale-network/tree/master/releases/mainnet' # URL of SM contracts ABI

local_ssl=false # optional, keep false to disable (for automated SSL setup)
```

4. Copy SKALE Manager ABI file for your network to `files/abi.json`
5. Copy Metaport config to `files/metaportConfig.json` - if you don't need Metaport - put `{}` in the file.
6. Setup proxy SSL certs: put certificate to `files/ssl/fullchain.pem` and private key to `files/ssl/privkey.pem`
7. Optional - setup explorer SSL certs: put explorer certificate to `files/ssl/explorer-0/fullchain.pem` and private key to `files/ssl/explorer-0/privkey.pem`

## 3. Usage

Once everything is in place, run:

```bash
ansible-playbook -i inventory main.yaml
```

## Contributing

**If you have any questions please ask our development community on [Discord](https://discord.gg/vvUtWJB).**

[![Discord](https://img.shields.io/discord/534485763354787851.svg)](https://discord.gg/vvUtWJB)

## License

![GitHub](https://img.shields.io/github/license/skalenetwork/skale.py.svg)

All contributions are made under the [GNU Lesser General Public License v3](https://www.gnu.org/licenses/lgpl-3.0.en.html). See [LICENSE](LICENSE).