# ReplicaSera WriteLib

this fork of replica adds serialised writelibs using the sera serdes library ([inspired from this post](https://devforum.roblox.com/t/replica-server-to-client-state-replication-module/3216980/179))

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
## new implementation:
supports fn and schema pairs

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

### note: both implementations can be used!!!
