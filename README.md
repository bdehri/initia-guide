# Initia 

Video: https://www.youtube.com/watch?v=M1WrZEFylzQ&feature=youtu.be

## Önkoşullar

* CPU: 4 çekirdek
* Bellek: 16GB
* Disk: 1000GB

Bu kurulum için contabo VPS 3 kullanıyorum.

## Kurulum

1. Ekran Oturumu Oluştur (Opsiyonel ama Tavsiye Edilir)

Komutun bir süre çalışacağı için bir screen oturumu oluşturmanızı şiddetle tavsiye ederim.

```
apt install screen
screen -S initia
```

Aynı oturuma bağlanmak için aşağıdaki komutu çalıştırmalısınız:

```bash
screen -r -d initia
```

2. Scripti İndir ve Çalıştır

Scripti indirin, çalıştırılabilir hale getirin ve ardından monikerinizle çalıştırın.

```bash
curl -OJL https://raw.githubusercontent.com/bdehri/initia-guide/main/initia_installer.sh
chmod +x initia_installer.sh
./initia_installer.sh <moniker>
```

3. Cüzdan Oluştur ve Token Al

```bash
source .bashrc
initiad keys add <anahtar-adı>
```

Bu noktada seedi yedeklemeyi unutmayın.

Tokenları [faucet](https://faucet.testnet.initia.xyz/) adresinden alabilirsiniz.

Örnek Komut:

```bash
initiad keys add robodehritest2
```

4. Logları Kontrol Et

```bash
journalctl -fu initiad
```

Node durumu için:

```bash
source .bashrc
initiad status | jq .sync_info
```

Catching Up: false olana kadar bekleyin.

5. Validator Oluştur

```bash
initiad tx mstaking create-validator \
    --amount="1000000uinit" \
    --pubkey=$(initiad tendermint show-validator) \
    --moniker="<moniker>" \
    --chain-id="initiation-1" \
    --from="<anahtar_adı>" \
    --commission-rate="0.10" \
    --commission-max-rate="0.20" \
    --commission-max-change-rate="0.01"
    --fees 30000uinit
```

Validator'unuzu [explorer](https://scan.testnet.initia.xyz/initiation-1) adresinden kontrol edebilirsiniz.

Örnek Komut:
```bash
initiad tx mstaking create-validator \
    --amount="20000000uinit" \
    --pubkey=$(initiad tendermint show-validator) \
    --moniker="robodehritest13" \
    --chain-id="initiation-1" \
    --from="robodehrimain" \
    --commission-rate="0.10" \
    --commission-max-rate="0.20" \
    --commission-max-change-rate="0.01"
    --fees 30000uinit
```



## SSS

### 1. `cosmovisor not found` ya da `initiad not found` benzeri hatalar nasıl çözülür?

PATH değişkeniniz güncel değil demektir. Aşağıdaki 2 komuttan birini çalıştırarak sorunu giderebilirsiniz.

```bash
source .bashrc
```

```bash
export PATH=$PATH:/usr/local/go/bin:/root/go/bin
```

### 2. `key not found` veya `account not found` benzeri hatalar nasıl çözülür?

* Videoda da bahsettiğim gibi eğer cüzdanınızda hiç hareket yoksa adresiniz cüzdan üzerinde yaratılmaz. Token aldıktan sonra bu hata geçecektir.
* Eğer cüzdanınızda token var ise, muhtemelen nodeunuz daha sync olmadı. Node sync olana kadar bekleyin ve tekrar deneyin.

## Prequisites

* CPU: 4 cores
* Memory: 16GB
* Disk: 1000GB

I am using contabo VPS 3 instance for this setup. 

## Installation

1. Create Sreen Session (Optional but Recommended)

I highly recommend to create a screen session to run the script as it takes a while.

```
apt install screen
screen -S initia
```

To connect to same session, you should run:

```bash
screen -r -d initia
```

2. Download and Run the Script

Download the script and make it executable, then run it with your moniker.

```bash
curl -OJL https://raw.githubusercontent.com/bdehri/initia-guide/main/initia_installer.sh
chmod +x initia_installer.sh
./initia_installer.sh <moniker>
```

3. Create Wallet and Get Some Tokens

```bash
source .bashrc
initiad keys add <key-name>
```

Do not forget to backup the seed at this point.

You can get tokens from [faucet](https://faucet.testnet.initia.xyz/).

Example Command:

```bash
initiad keys add robodehritest2
```

4. Check Logs

```bash
journalctl -fu initiad
```

For node status:

```bash
source .bashrc
initiad status | jq .sync_info
```
Wait until Catching Up: false 

4. Create Validator

```bash
initiad tx mstaking create-validator \\
    --amount="1000000uinit" \\
    --pubkey=$(initiad tendermint show-validator) \\
    --moniker="<moniker>" \\
    --chain-id="initiation-1" \\
    --from="<key_name>" \\
    --commission-rate="0.10" \\
    --commission-max-rate="0.20" \\
    --commission-max-change-rate="0.01"
    --fees 30000uinit
```

You can check your validator from [explorer](https://scan.testnet.initia.xyz/initiation-1).

Example Command:
```bash
initiad tx mstaking create-validator \
    --amount="20000000uinit" \
    --pubkey=$(initiad tendermint show-validator) \
    --moniker="robodehritest13" \
    --chain-id="initiation-1" \
    --from="robodehrimain" \
    --commission-rate="0.10" \
    --commission-max-rate="0.20" \
    --commission-max-change-rate="0.01"
    --fees 30000uinit
```
