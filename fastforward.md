### Fastforward
Find where `GameTime` class is used. One of the usages is class like
```
// Token: 0x02000106 RID: 262
public sealed class e5e
{
	// Token: 0x060006B3 RID: 1715 RVA: 0x0001B0A0 File Offset: 0x000192A0
	public GameTime a()
	{
		return this.a;
	}

	// Token: 0x060006B4 RID: 1716 RVA: 0x0001B0A8 File Offset: 0x000192A8
	public MouseState b()
	{
		return this.b;
	}

	// Token: 0x060006B5 RID: 1717 RVA: 0x0001B0B0 File Offset: 0x000192B0
	public KeyboardState c()
	{
		return this.c;
	}

	// Token: 0x060006B6 RID: 1718 RVA: 0x0001B0B8 File Offset: 0x000192B8
	public e5e(GameTime A_0, MouseState A_1, KeyboardState A_2)
	{
		this.b = A_1;
		this.c = A_2;
		this.a = A_0;
	}

	// Token: 0x04000406 RID: 1030
	private GameTime a;

	// Token: 0x04000407 RID: 1031
	private MouseState b;

	// Token: 0x04000408 RID: 1032
	private KeyboardState c;

	// Token: 0x04000409 RID: 1033
	public bool d = true;
}
```
In the constructor look at the argument of type `GameTime` and where it is assigned to the field (`this.a = A_0;` in this case). Use il editor to change it to something like
```
this.a = Mods.ApplyFastforward(A_0);
```
