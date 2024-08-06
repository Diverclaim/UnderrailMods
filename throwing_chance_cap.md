### Throwing chance cap
Look for constant 0,9, find usage with 3 constants in a row:
```
else
{
    num = 1.0;
}
array[0] = d0m.b(0.15, 0.4 - (A_2 - 1.5) * 0.05 + (double)A_1 * 0.0075 + A_3, 0.9) * num;
array[1] = d0m.b(0.15, 0.6 - (A_2 - 1.5) * 0.05 + (double)A_1 * 0.0075 + A_3, 0.9) * num;
array[2] = d0m.b(0.15, 0.8 - (A_2 - 1.5) * 0.05 + (double)A_1 * 0.0075 + A_3, 0.9) * num;
if (array[1] == array[0])
{
    array[1] += (1.0 - array[0]) / 3.0;
    array[2] = array[1] + (1.0 - array[0]) / 3.0;
}
```
Change it to this:
```
else
{
    num = 1.0;
}
array[0] = d0m.b(0.15, 0.4 - (A_2 - 1.5) * 0.05 + (double)A_1 * 0.0075 + A_3, Mods.ApplyThrowingChanceCap(0.9)) * num;
array[1] = d0m.b(0.15, 0.6 - (A_2 - 1.5) * 0.05 + (double)A_1 * 0.0075 + A_3, Mods.ApplyThrowingChanceCap(0.9)) * num;
array[2] = d0m.b(0.15, 0.8 - (A_2 - 1.5) * 0.05 + (double)A_1 * 0.0075 + A_3, Mods.ApplyThrowingChanceCap(0.9)) * num;
if (array[1] == array[0])
{
    array[1] += (1.0 - array[0]) / 3.0;
    array[2] = array[1] + (1.0 - array[0]) / 3.0;
}
```