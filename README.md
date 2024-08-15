# Evmos Devnet

Use this repo to start a Evmos Devnet compose of 4 nodes:

- `evmos-devnet1`
- `evmos-devnet2`
- `evmos-devnet3`
- `evmos-devnet4`

Note: `[default v9.1.0]`

## NOTE: This repository has moved: https://github.com/evmos/testing


## Customize

You can update the commits to be tested by updating `commit_hash` for the respective evmos-devnet nodes in `docker-compose.yml`. 

## Run

To run the localnet setup, start the docker containers (defined in [docker-compose.yml](https://github.com/facs95/devops/blob/main/docker-compose.yml)) using

```bash 
docker compose --profile nodes --profile metrics --profile bots up --build -d
```

It is also possible to start services seperately. The docker file splits services with using following profiles:

nodes -> Spins up blockchain nodes

metrics -> Spins up metrics capability 

bots -> Spins up bots to send tx to nodes

Hence in a case where starting nodes seperately is required, run:

```bash 
docker compose --profile nodes up --build -d
```
.viz likewise for metrics and bots

To get the log outputs for individual services (e.g. the individual Evmos nodes), you can specify the service to be printed to the terminal output by adding this as an argument to the `docker compose logs` command, e.g.

```bash
docker compose logs evmos-node-1 -f
```

If you want to stop the execution of the testing setup, use

```bash
docker compose --profile nodes --profile metrics --profile bots down
```

## Tx-bot

Transaction bots are refernced via submodule to the following repository  [here](https://github.com/evmos/bots)


Bots submit tx on the network using the account specified in the `start.sh` - by default private key is the same for all instances of the tx bot and the bot uses our JSON-RPC API which is exposed on port `8545`.

see [docker-compose.yml](https://github.com/Leon-Africa/evmosdevops/blob/main/docker-compose.yml).

There is one tx bot per node.

- `tx-botn` -> `evmos-devnetn` where n is 1 to max number nodes 

Note: `[default 4 nodes]`

# Containers

Nodes:

| Name          | IP        | Ports                    |
| ------------- | ----------| -------------------------|
| evmos-node-1  | 10.7.7.2  | 8545:8545 / 26660:26660  |
| evmos-node-2  | 10.7.7.3  | 8546:8545 / 26661:26660  |
| evmos-node-3  | 10.7.7.4  | 8547:8545 / 26662:26660  |
| evmos-node-4  | 10.7.7.5  | 8548:8545 / 26663:26660  |

Metrics:

In browser use ````localhost```` as IP

| Name          | IP            | Ports         |
| ------------- | ------------- | ------------- |
| node-exporter | 10.7.7.6      | 9100:9100     |
| prometheus    | 10.7.7.7      | 9090:9090     |
| alertmanager  | 10.7.7.8      | 9093:9093     |
| cadvisor      | 10.7.7.9      | 8080:8080     |
| phlare        | 10.7.7.10      | 4100:4100     |
| grafana       | 10.7.7.11      | 3000:3000     |

Bots:

| Name          | IP            | Ports         |
| ------------- | ------------- | ------------- | 
| tx-bot-1      | 10.7.7.12     | 8081:8080     | 
| tx-bot-2      | 10.7.7.13     | 8082:8080     | 
| tx-bot-3      | 10.7.7.14     | 8083:8080     | 
| tx-bot-4      | 10.7.7.15     | 8084:8080     |
