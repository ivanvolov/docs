# DeltaResolver
[Git Source](https://github.com/uniswap/v4-periphery/blob/ea2bf2e1ba6863bb809fc2ff791744f308c4a26d/src/base/DeltaResolver.sol) - Generated with [forge doc](https://book.getfoundry.sh/reference/forge/forge-doc)

**Inherits:**
[ImmutableState](contracts/v4/reference/periphery/base/ImmutableState.md)

Abstract contract used to sync, send, and settle funds to the pool manager

*Note that sync() is called before any erc-20 transfer in `settle`.*


## Functions
### _take

Take an amount of currency out of the PoolManager

*Returns early if the amount is 0*


```solidity
function _take(Currency currency, address recipient, uint256 amount) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`currency`|`Currency`|Currency to take|
|`recipient`|`address`|Address to receive the currency|
|`amount`|`uint256`|Amount to take|


### _settle

Pay and settle a currency to the PoolManager

*The implementing contract must ensure that the `payer` is a secure address*

*Returns early if the amount is 0*


```solidity
function _settle(Currency currency, address payer, uint256 amount) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`currency`|`Currency`|Currency to settle|
|`payer`|`address`|Address of the payer|
|`amount`|`uint256`|Amount to send|


### _pay

Abstract function for contracts to implement paying tokens to the poolManager

*The recipient of the payment should be the poolManager*


```solidity
function _pay(Currency token, address payer, uint256 amount) internal virtual;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token`|`Currency`|The token to settle. This is known not to be the native currency|
|`payer`|`address`|The address who should pay tokens|
|`amount`|`uint256`|The number of tokens to send|


### _getFullDebt

Obtain the full amount owed by this contract (negative delta)


```solidity
function _getFullDebt(Currency currency) internal view returns (uint256 amount);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`currency`|`Currency`|Currency to get the delta for|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amount`|`uint256`|The amount owed by this contract as a uint256|


### _getFullCredit

Obtain the full credit owed to this contract (positive delta)


```solidity
function _getFullCredit(Currency currency) internal view returns (uint256 amount);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`currency`|`Currency`|Currency to get the delta for|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amount`|`uint256`|The amount owed to this contract as a uint256|


### _mapSettleAmount

Calculates the amount for a settle action


```solidity
function _mapSettleAmount(uint256 amount, Currency currency) internal view returns (uint256);
```

### _mapTakeAmount

Calculates the amount for a take action


```solidity
function _mapTakeAmount(uint256 amount, Currency currency) internal view returns (uint256);
```

### _mapWrapUnwrapAmount

Calculates the sanitized amount before wrapping/unwrapping.


```solidity
function _mapWrapUnwrapAmount(Currency inputCurrency, uint256 amount, Currency outputCurrency)
    internal
    view
    returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`inputCurrency`|`Currency`|The currency, either native or wrapped native, that this contract holds|
|`amount`|`uint256`|The amount to wrap or unwrap. Can be CONTRACT_BALANCE, OPEN_DELTA or a specific amount|
|`outputCurrency`|`Currency`|The currency after the wrap/unwrap that the user may owe a balance in on the poolManager|


## Errors
### DeltaNotPositive
Emitted trying to settle a positive delta.


```solidity
error DeltaNotPositive(Currency currency);
```

### DeltaNotNegative
Emitted trying to take a negative delta.


```solidity
error DeltaNotNegative(Currency currency);
```

### InsufficientBalance
Emitted when the contract does not have enough balance to wrap or unwrap.


```solidity
error InsufficientBalance();
```

