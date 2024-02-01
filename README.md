# babylon

Sistem Gereksinimleri

Bileşenler	Minimum Gereksinimler

CPU	4

RAM	8 GB

Storage	250 GB SSD

Script ile kurlum için aşağıdaki komutu girin

curl -sSL -o babylon-kurulum.sh https://raw.githubusercontent.com/Core-Node-Team/Testnet-TR/main/Babylon/babylon.sh && chmod +x babylon-kurulum.sh && bash ./babylon-kurulum.sh

Manuel kurulum yapmak isteyenler için Link

Kurulumu tamamladıktan sonra bu komutu girin

source $HOME/.bash_profile

Cüzdan oluşturun

Mnemonic kaydedip saklayın

babylond keys add wallet

Faucet

Babylon Discorda gidip #faucet kanalından !faucet cüzdanadresi ile test tokenlarını alın

BLS key oluşturun

babylond create-bls-key $(babylond keys show wallet -a)

Ardından yeni oluştuırulan BLS keyinb belleğe yüklenebilmesi için nodeyi yeniden başlatmak gerekiyor

sudo systemctl restart babylond

Yapılandırma ayarlarını değiştirin

BLS imza işlemlerini gönderecek key ismini belirtmek gerekiyor

Cüzdan ismini wallet yerine başka bir isim yaptıysanız komutu değiştirin

sed -i -e "s|^key-name *=.*|key-name = \"wallet\"|" $HOME/.babylond/config/app.toml

Validatörün yeni bloğa başlamadan önce bekleyeceği süreyi belirtin

Babylon ağında bloklar arası 10 saniye süre olması hedefleniyor

sed -i -e "s|^timeout_commit *=.*|timeout_commit = \"10s\"|" $HOME/.babylond/config/config.toml

Validatör

Senkronizasyon durumunuzu kontrol edin

babylond status 2>&1 | jq .SyncInfo

Ulaştığınız blok yüksekliğini Explorer ile karşılaştırın. Senkronize olduktan sonra "catching_up": false çıktısı verir

babylond tx checkpointing create-validator \

 --amount="1000000ubbn" \
 
 --pubkey=$(babylond tendermint show-validator) \
 
 --moniker $MONİKER \
 
 --website "WEBSİTENİZ" \
 
 --identity KEYBASE.İO İD \
 
 --details "Core Node Community" \
 
 --chain-id bbn-test-2 \
 
 --gas="auto" \
 
 --gas-adjustment 1.2 \
 
 --gas-prices "0.0025ubbn" \
 
 --keyring-backend=test \
 
 --from wallet \
 
 --commission-rate "0.10" \
 
 --commission-max-rate "0.20" \
 
 --commission-max-change-rate "0.01" \
 
 --min-self-delegation "1" \
 
 -y

Faydalı Linkler

Komutlar

Node Yedekleme ve Taşıma

Port Değiştirme

Sync-Peer-FAQ
