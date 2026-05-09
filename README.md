# ReplicaSera Compatibility

this fork adds compatibility with sera and replica specifically for your writelib

## original implementation:

```lua
WriteLib.AddMoney = function( replica, amount )
    local NewAmount = math.max(0, replica.Data.Money + amount)
    replica:Set({ "Money" }, NewAmount)
    return NewAmount
end

```
### calling it:
```lua
replica:Write("AddMoney", amount)
```
## new implementatiion:

```lua
WriteLib.AddMoney = {
	Schema = Sera.Schema({
		Amount = Sera.Uint32,
	}),
	Fn = function( replica, args )
		local NewAmount = math.max(0, replica.Data.Money + args.Amount)
		replica:Set({ "Money" }, NewAmount)
		return NewAmount
	end,
}

```
### calling it:
```lua
replica:Write("AddMoney", { Amount = amount })
```

### note: both implementations can be used in the same writelib!!!
