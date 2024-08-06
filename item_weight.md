### Item weight
Search for property SingleItemWeight, something like this should be found:
```
// Token: 0x1700001B RID: 27
// (get) Token: 0x060000CD RID: 205 RVA: 0x00004FE9 File Offset: 0x000031E9
public double SingleItemWeight
{
    get
    {
        if (this.Definition != null)
        {
            return this.Definition.a3();
        }
        return 0.0;
    }
}
```
Use il editor to change it to
```
// Token: 0x1700001B RID: 27
// (get) Token: 0x060000CD RID: 205 RVA: 0x00004FE9 File Offset: 0x000031E9
public double SingleItemWeight
{
    get
    {
        if (this.Definition != null)
        {
            return Mods.ApplySingleItemWeight(this.Definition.a3());
        }
        return 0.0;
    }
}
```