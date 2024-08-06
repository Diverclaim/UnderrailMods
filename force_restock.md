### Force restock
Look for string "iMRCH", you will find it in attribute on interface. Look for implementations of this interface, there should be only 1 such class, and in this class a method like this:
```
// Token: 0x06006CF4 RID: 27892 RVA: 0x002CDE98 File Offset: 0x002CC098
public void apm(bool A_0 = false)
{
    if (this.a == null)
    {
        this.a = new dcb();
    }
    if (string.IsNullOrEmpty(this.b))
    {
        duh.b(LogSeverity.Warning, "Merchant '{0}' does not have a store set.", new object[] { base.a8().ToString() });
        return;
    }
    bool flag = false;
    qa qa = c7x.a(this.b);
    if (qa == null)
    {
        duh.b(LogSeverity.Warning, "Failed to retrieve store '{0}' for merchant '{1}'.", new object[]
        {
            this.g(),
            base.a8().ToString()
        });
        return;
    }
    cm1 serviceOrThrow = bpa.GetServiceOrThrow<cm1>();
    double num = 1.0;
    if (serviceOrThrow.ap6() != null && serviceOrThrow.ap6().u() != null && serviceOrThrow.ap6().u().Feats.Contains<pg>())
    {
        num += pg.a * (double)serviceOrThrow.ap6().u().Skills.Get<e62>().g();
    }
    if (serviceOrThrow.ap6() != null && serviceOrThrow.ap6().u() != null && serviceOrThrow.ap6().u().Feats.Contains<pg>() && !this.j)
    {
        this.j = true;
        foreach (cnz cnz in this.a.zb())
        {
            if (num != 1.0 && cnz.Definition != null && cnz.Definition.a4() != null && this.apk() != null && this.apk().Contains(cnz.Definition.a4()))
            {
                cnz.Stacks = (int)((double)cnz.Stacks * num);
            }
        }
    }
    if (serviceOrThrow.ap6() != null && (qa.c() != null || A_0) && (A_0 || serviceOrThrow.ap6().p() > this.h))
    {
        this.f();
        this.h = serviceOrThrow.ap6().p() + TimeSpan.FromMinutes((double)qa.c().Value);
        this.a();
        flag = true;
    }
    zp.a = new Random(this.l * this.k * serviceOrThrow.ap6().l());
    iv iv = qa.a(this);
    if (iv != null)
    {
        if (iv.a)
        {
            this.f();
            this.h = serviceOrThrow.ap6().p() + TimeSpan.FromMinutes((double)qa.c().Value);
            this.a();
            flag = true;
        }
        else if (iv.b)
        {
            this.a();
        }
        if (iv.d != null && iv.d.Count > 0)
        {
            this.c.AddRange(iv.d);
            this.k++;
        }
        if (iv.c != null && iv.c.Count > 0)
        {
            flag = true;
            foreach (cnz cnz2 in iv.c)
            {
                if (cnz2 != null)
                {
                    if (num != 1.0 && cnz2.Definition != null && cnz2.Definition.a4() != null && this.apk() != null && this.apk().Contains(cnz2.Definition.a4()))
                    {
                        cnz2.Stacks = (int)((double)cnz2.Stacks * num);
                    }
                    this.a.zc(cnz2, true);
                }
            }
        }
    }
    if (flag)
    {
        this.b(qa);
        return;
    }
    this.a(qa);
}
```
Add code in the beginning like this:
```
// Token: 0x06006CF4 RID: 27892 RVA: 0x002CDE98 File Offset: 0x002CC098
public void apm(bool A_0 = false)
{
    A_0 = Mods.ApplyForceRestock(A_0);
    if (this.a == null)
    {
        this.a = new dcb();
    }
    if (string.IsNullOrEmpty(this.b))
    {
        duh.b(LogSeverity.Warning, "Merchant '{0}' does not have a store set.", new object[] { base.a8().ToString() });
        return;
    }
```