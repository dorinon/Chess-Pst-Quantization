# Chess-Pst-Quantization
Quantization for chess piece square tables for pesto and other tables

##Configurations  
```cs
private static readonly int[][] PstsArray = //your psts of choice already set to pesto psts

//                           mg:  P    K    B    R    Q    K  eg: P    K    B    R    Q     K
private static int[] pieceVal = { 100, 320, 330, 500, 900, 20000, 100, 320, 330, 500, 900, 20000 }; // your piece val can be different for mg and eg needed to make the minimum of all psts 0
private static readonly float commpressAmount = // absolute highset value in your psts / 128
```

##Unpacking 
to unpack in your own code you can just copy the UnpackToInt function.  
but if you want to make it more compact you can unpack this way:
```cs
int[] unpackedPsts = new int[64 * 12];
for (int i = 0; i < 64 * 12; i++)
{
  unpackedPsts[i] = (int)(((BigInteger)quantizedArray[i] >> (j * 8)) & 255) * commpressAmount;
}
```
notice this will fill the whole array even if you didnt use 12 tables and every 12 values represent the same square position in the psts.
