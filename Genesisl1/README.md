# Snaphot 15.09.22 (69 GB) height 4242606
```bash
# install the node as standard, but do not launch. Then we delete the .data directory and create an empty directory
systemctl stop genesisd
rm -rf $HOME/.genesisd/data/
mkdir $HOME/.genesisd/data/

# download archive
cd $HOME
wget http://51.222.244.75:6001/genesisddata.tar.gz

# unpack the archive
tar -C $HOME/ -zxvf genesisddata.tar.gz --strip-components 1
# !! IMPORTANT POINT. If the validator was created earlier. Need to reset priv_validator_state.json  !!
wget -O $HOME/.genesisd/data/priv_validator_state.json "https://raw.githubusercontent.com/obajay/StateSync-snapshots/main/priv_validator_state.json"
cd && cat .genesisd/data/priv_validator_state.json
{
  "height": "0",
  "round": 0,
  "step": 0
}

# after unpacking, run the node
# don't forget to delete the archive to save space
cd $HOME
rm genesisddata.tar.gz
systemctl restart genesisd && journalctl -u genesisd -f -o cat
```
