#  BO2 Killfeed Hook Example
Hook used to create custom Killfeed in Cod Bo2
## 360 Address
```
CL_ConsolePrint_AddLineHook = 0x82267520
```
## Hook Example
```cpp
void CL_ConsolePrint_AddLineHook(int localClientNum, int channel, const char* txt, int duration, int pixelWidth, int color, int flags)
{
	if (channel == 6)
	{
		char killer[64] = {};
		char weapon[64] = {};
		char victim[64] = {};
		char reason[128] = {};
		BOOL special = FALSE;

		if (Killfeed::ParseMessage(txt, killer, weapon, victim, reason, &special))
		{
			Killfeed::Add(killer, weapon, victim, reason, special);
			return;
		}
	}
	CL_ConsolePrint_AddLineDetour->callOriginal(localClientNum, channel, txt, duration, pixelWidth, color, flags);
}
```
## What it could look like
[![Link](https://img.youtube.com/vi/sc2MHtLe_1Q/hqdefault.jpg)](https://youtu.be/sc2MHtLe_1Q)
