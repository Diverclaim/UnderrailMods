### Traders buy all
Search for string "Trade", you should find usage like this:
```
this.k.Text = "Trade";
```
Look for usages of field `k` (in this case), you are interested in this:
```
this.k.Enabled = flag && num >= num2 && !flag2;
```
Just above it there is something like this:
```
bool flag2 = this.c();
```
Jump into method `c()`, and add changes in the beginning so it looks something like this:
```
// Token: 0x06002445 RID: 9285 RVA: 0x000C9ADC File Offset: 0x000C7CDC
private bool c()
{
    if (Mods.IsTradersBuyAllEnabled())
    {
        return false;
    }
    bool flag = false;
    this.u.Clear();
    if (this.c != null)
    {
        Dictionary<a0, int> dictionary = new Dictionary<a0, int>(this.c.apl());
        foreach (cnz cnz in this.g.l().zb())
        {
            if (!this.r.Contains(cnz.Definition.a4()) && cnz.Definition.bg() != global::a0.b)
            {
                int num;
                if (!dictionary.TryGetValue(cnz.Definition.bg(), out num))
                {
                    flag = true;
                    this.u.Add(cnz);
                }
                else if (num != -1)
                {
                    if (cnz.Stacks > num)
                    {
                        flag = true;
                        this.u.Add(cnz);
                    }
                    else
                    {
                        num -= cnz.Stacks;
                        if (num == 0)
                        {
                            dictionary.Remove(cnz.Definition.bg());
                        }
                        else
                        {
                            dictionary[cnz.Definition.bg()] = num;
                        }
                    }
                }
            }
        }
    }
    return flag;
}
```
In the same class look for method that has string "I'm currently looking to buy" in it. Also change it so there is a condition in the beginning:
```
// Token: 0x06002442 RID: 9282 RVA: 0x000C94E4 File Offset: 0x000C76E4
private new void e()
{
    if (Mods.IsTradersBuyAllEnabled())
    {
        return;
    }
    wj wj = wj.a();
    string text;
```
In the same class look for method like this:
```
// Token: 0x0600243F RID: 9279 RVA: 0x000C93CC File Offset: 0x000C75CC
public bool adk(cnz A_0)
{
    return A_0 != null && A_0.ItemValue != 0 && (A_0.Definition.bg() == global::a0.b || (this.r != null && this.r.Contains(A_0.Definition.a4())) || (this.t != null && this.t.Contains(A_0.Definition.bg())));
}
```
Using il editor add condition to the beginning like in other cases:
```
// Token: 0x0600243F RID: 9279 RVA: 0x000C93CC File Offset: 0x000C75CC
public bool adk(cnz A_0)
{
    return !Mods.IsTradersBuyAllEnabled() && (A_0 != null && A_0.ItemValue != 0) && (A_0.Definition.bg() == global::a0.b || (this.r != null && this.r.Contains(A_0.Definition.a4())) || (this.t != null && this.t.Contains(A_0.Definition.bg())));
}
```