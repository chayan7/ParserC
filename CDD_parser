#Author: Chayan Kumar Saha

import argparse
import re


usage= '''  Description: Parse output from NCBI CDD server '''


parser = argparse.ArgumentParser(description=usage)
parser.add_argument("-c", "--cdd", required=True, help="CDDhit_output")
parser.add_argument("-v","--version", action="version", version='%(prog)s 3.4.6')
args = parser.parse_args()
parser.parse_args()

'''

#Query	Hit type	PSSM-ID	From	To	E-Value	Bitscore	Accession	Short name	Incomplete	Superfamily	Code
Q#1 - WP_011007711.1	specific	338659	25	130	2.55529e-06	43.7806	pfam13274	DUF4065	 - 	cl01445	d4065


'''



hitDict={}

h=0
hitSet=set()
with open (args.cdd, 'r') as fileIn:
	for line in fileIn:
		if line[:2]=='Q#':
			h+=1
			Line=line.rstrip().split('\t')
			accIds=Line[0].replace(' ','').replace('(Warning:thissequencerecordmaybeobsoleteorpreliminary)','').split('-')[1]
			hitSet.add(accIds)
			hitDict[accIds+':'+str(h)]=Line[-3]

hitDict_combined={}
for ids in hitSet:
	hitName=set()
	for acc in hitDict:
		if acc.split(':')[0]==ids:
			hitName.add(hitDict[acc])
	hitDict_combined[ids]='_'.join(map(str,hitName))

i=0
with open ('CDDoutParsed.txt', 'w') as out:
	for ids in hitDict_combined:
		i+=1
		print(i, ids.replace('>',''), hitDict_combined[ids], sep='\t', file=out)
