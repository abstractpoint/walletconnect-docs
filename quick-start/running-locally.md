---
description: Guide for getting all the components for WalletConnect running locally
---

# Running Locally

## Set up local Node Bridge

```
git clone https://github.com/WalletConnect/node-walletconnect-bridge.git
cd node-walletconnect-bridge
git checkout v0.8.x
npm install
```

Install Redis
{% tabs %}
{% tab title="OS X" %}
prerequisite to have [brew](https://brew.sh/)
```
brew install redis
```
{% endtab %}
{% tab title="Ubuntu" %}
```
sudo apt update
sudo apt install redis-server
```
{% endtab %}
{% endtabs %}

Start redis
```
redis-server
```
