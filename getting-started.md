## Otterscan, a An open-source, fast, local, laptop-friendly Ethereum block explorer.
 
 
### Erigon settings
When running erigon, make sure to enable the erigon, ots, eth APIs in addition to whatever cli options you are using to start erigon. It should at least look like this `--http.api "eth,erigon,ots,<your-other-apis>"`
This is to be added to the config of your Erigon package under `"EXTRA_OPTS"`

### Consensus Client settings
If you wish Otterscan to also display beacon chain data, you'll need to adjust the 'Access-Control-Allow-Origin' setting on your Consensus Client. Here's a few examples, but you should always refer to their own documentation:

- Prysm:
In Config, Advanced, Beacon Chain, CORSDOMAIN, add `",*"` at the end of the config to enable requests to the REST API. keeping the current default setting, it should look like this `http://prysm.dappnode,*`
After doing this, in the Otterscan settings, use `http://beacon-chain.prysm.dappnode:3500` as the `BEACON_API_URL`

- Nimbus:
In Config, Advanced, add `--rest-allow-origin=*` to the `EXTRA_OPTS` field.
After doing this, in the Otterscan settings, use `http://nimbus.dappnode:4500` as the `BEACON_API_URL`

- Lighthouse:
In the Otterscan settings, use `http://beacon-chain.lighthouse.dappnode:3500` as the `BEACON_API_URL`

- Teku:
In the Otterscan settings, use `http://beacon-chain.teku.dappnode:3500` as the `BEACON_API_URL`

- Lodestar:
In the Otterscan settings, use `http://beacon-chain.lodestar.dappnode:3500` as the `BEACON_API_URL`
