# noderunner
# Starknet
sudo apt update -y && sudo apt install apt-transport-https ca-certificates curl software-properties-common -y && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" && sudo apt install docker-ce

sudo apt-get install -y pkg-config curl git build-essential libssl-dev screen

git clone --branch v0.4.0 https://github.com/eqlabs/pathfinder.git

sudo docker pull eqlabs/pathfinder

docker logs -f starknet
mkdir -p $HOME/pathfinder
docker run -d \
  --rm \
  -p 9545:9545 \
  --user "$(id -u):$(id -g)" \
  -e RUST_LOG=info \
  --name starknet \
  -e PATHFINDER_ETHEREUM_API_URL="https://eth1.lava.build/lava-referer-f8e556e6-0e36-4b79-86ed-2f048dcf4c19" \
  -v $HOME/pathfinder:/usr/share/pathfinder/data \
  eqlabs/pathfinder
