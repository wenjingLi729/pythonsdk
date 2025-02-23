# pythonsdk

# requirements
    python2.7 python3.x

    ecdsa
    requests
  
# quick start
    pip install xuper

## start server
    nohup ./xchain &
    nohup ./xchain-httpgw &

## A wallet demo on python sdk
![WalletDemo](https://github.com/xuperchain/pythonsdk/blob/master/images/wallet.png)

## Demo of python SDK
  ```
  pysdk = xuper.XuperSDK("http://localhost:8098", "xuper")
  pysdk.readkeys("./data/keys")

  #1. 普通转账
  pysdk.transfer("bob", 88888, desc="hello world")

  #2. 创建合约账号
  new_account_name = pysdk.new_account()
  print("wait acl confirmed....")
  time.sleep(3)

  #3. 部署合约
  pysdk.transfer(new_account_name, 10000000, desc="start funds")
  pysdk.set_account(new_account_name)
  contract_name = 'counter'+str(random.randint(100,1000000))
  print("deploying......")
  rsps = pysdk.deploy(new_account_name, contract_name, open('./data/wasm/counter.wasm','rb').read(), {'creator':b'baidu'})
  print(rsps)

  #4. 预执行合约
  rsps = pysdk.preexec(contract_name, "get", {"key":b"counter"})
  print(rsps.decode())

  #5. 调用合约并生效上链
  for i in range(5):
          rsps = pysdk.invoke(contract_name, "increase", {"key":b"counter"})
          print(rsps)

```
