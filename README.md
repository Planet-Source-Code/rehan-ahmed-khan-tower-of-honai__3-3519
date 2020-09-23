<div align="center">

## tower of honai


</div>

### Description

in recursion we have limited stack to keep data.

so when we try to find the solution of tower of honai for 5, we get in trouble. to solve this problem we've non recursive solution of it.
 
### More Info
 
it take only one input.(number of plates u have)

nothing special. but i'll be better if he knows about recursive solution of tower of honai.

it returns all the movement of the plates b/w the towers


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Rehan Ahmed Khan](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/rehan-ahmed-khan.md)
**Level**          |Advanced
**User Rating**    |5.0 (10 globes from 2 users)
**Compatibility**  |C, C\+\+ \(general\), Microsoft Visual C\+\+, Borland C\+\+
**Category**       |[Data Structures](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/data-structures__3-8.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/rehan-ahmed-khan-tower-of-honai__3-3519/archive/master.zip)





### Source Code

```
#include <iostream.h>
#include <math.h>
#define ARRAYSIZE 100
/*************************************************************************************************
           PROGRAMMED BY : REHAN AHMED KHAN
                   PAKISTAN- KARACHI
                   BS student in FAST University
                   (foundation for advancement of science and technology)
      this program is free ware and anyone can use it.
/************************************************************************************************/
/*************************************************************************************************
*								THE ALGORITHM USED IS AS FOLLOWS								 *
*																								 *
*	Because the tree is complete it can be stored in an array of 2^n-1.							 *
*	The root of the tree is in position 2^(n-1)-1												 *
*	For any level j, the first node at that level is in position 2^(n-1-j)-1					 *
*	and each successive node at that level is 2^(n-j) elements beyond the previous element		 *
*	at that level																				 *
*	So the sequential traversal of the array produces the solution of Towers of Hanoi Problem	 *
*																								 *
*************************************************************************************************/
class TowersHanoi
{
	private:
		struct										//node structure
		{
			char chToPeg;
			char chFromPeg;
			int iDiskNo;
		}node[ARRAYSIZE];							//Array of Nodes
		char except(char chFromPeg, char chToPeg);	//returns peg other than provided as parameter
	public:
		TowersHanoi();								//constructor
		//generates the tree
		void generateTree(char chFromPeg,char chToPeg, int iDiskNo);
};
//////////////////////////////////////////////////////////////////////////////////////////////////
TowersHanoi::TowersHanoi()
{
	int iDiskNo;
	cout << "\nENTER THE NUMBER OF DISKS >> ";
	cin >> iDiskNo;
	generateTree('A','B',iDiskNo);
	int cMoves=(int)pow(2,iDiskNo)-1;
	cout << "THE MOVES ARE AS FOLLOWS\n";
	for(int i=0;i<cMoves;i++)
		cout << i+1 << ": " <<"Move Disk " << node[i].iDiskNo << " From " << node[i].chFromPeg
			 << " To " << node[i].chToPeg << endl;
}
//////////////////////////////////////////////////////////////////////////////////////////////////
void TowersHanoi::generateTree(char chFromPeg, char chToPeg, int iDiskNo)
{
	int j, iLevel=1, iDistance, iDistance2;
	int iNodeIndex;
	node[(int)pow(2,iDiskNo-1)-1].chToPeg=chToPeg;
	node[(int)pow(2,iDiskNo-1)-1].chFromPeg=chFromPeg;
	node[(int)pow(2,iDiskNo-1)-1].iDiskNo=iDiskNo;
	for(int i=1;i<=iDiskNo-1;i++)
	{
		iDistance=0;
		iDistance2=(int)pow(2,iDiskNo-i);
		for(j=0;j<(int)pow(2,i);j++)
		{
			if(j%2==0)
			{
				iNodeIndex=iDistance+(int)pow(2,iDiskNo-1-i)-1;
				node[iNodeIndex].chToPeg=
					except(node[iNodeIndex+iDistance2/2].chFromPeg,
						  node[iNodeIndex+iDistance2/2].chToPeg);
				node[iNodeIndex].chFromPeg=
					node[iNodeIndex+iDistance2/2].chFromPeg;
				node[iNodeIndex].iDiskNo=iDiskNo-iLevel;
			}
			else
			{
				iNodeIndex=iDistance+(int)pow(2,iDiskNo-1-i)-1;
				node[iNodeIndex].chFromPeg=
					except(node[iNodeIndex-iDistance2/2].chFromPeg,
						  node[iNodeIndex-iDistance2/2].chToPeg);
				node[iNodeIndex].chToPeg=
					node[iNodeIndex-iDistance2/2].chToPeg;
				node[iNodeIndex].iDiskNo=iDiskNo-iLevel;
			}
			iDistance+=(int)pow(2,iDiskNo-i);
		}
		iLevel++;
	}
}
//////////////////////////////////////////////////////////////////////////////////////////////////
char TowersHanoi::except(char chFromPeg, char chToPeg)
{
	if(chFromPeg=='A' && chToPeg=='B' || chFromPeg=='B' && chToPeg=='A')
		return 'C';
	if(chFromPeg=='A' && chToPeg=='C' || chFromPeg=='C' && chToPeg=='A')
		return 'B';
	if(chFromPeg=='B' && chToPeg=='C' || chFromPeg=='C' && chToPeg=='B')
		return 'A';
}
//////////////////////////////////////////////////////////////////////////////////////////////////
/*ostream& operator << (ostream& s,nodeHanoi node)
{
	return s <<"Move Disk " << node.iDiskNo << " From " << node.chFromPeg
		   << " To " << node.chToPeg << endl;
}*/
//////////////////////////////////////////////////////////////////////////////////////////////////
void main(void)
{
	cout << "A represents FROM PEG,\nB represents TO PEG,\nC represents AUXILLARY PEG\n";
	TowersHanoi towersHanoi;
}
```

