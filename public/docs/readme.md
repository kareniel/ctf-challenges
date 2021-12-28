# 100 ctf challenges docs

This is the docs for the 100 ctf challenges.


---

all instructions take their parameters from the stack
All instructions are encoded on 1 byte
with the exception of the PUSH1 instruction, which allows to put an arbitrary value on the stack and encode the value directly after the instruction
256 opcodes
The context is made of several memory regions, each with its own purpose


code region
read with CODESIZE and CODECOPY. 
also EXTCODESIZE and EXTCODECOPY?
empty for externally owned accounts, EOAs (users)


stack = list of 32-byte elements
memory = region only exists during the smart contract execution, accessed with a byte offset
the size is counted with the highest address that was accessed
generally read and written with MLOAD and MSTORE instructions
also CREATE or EXTCODECOPY etc

storage
map of the 32-byte slot to 32-byte value
each value written is kept until it is set to 0 or the contract self-destruction
Reading from an unset key also returns 0
read and written with the instructions SLOAD and SSTORE

calldata
data sent with a transaction
for contract creation, the constructor code
immutable 
read with  CALLDATALOAD, CALLDATASIZE, and CALLDATACOPY.

returndata
return a value after a call
can be set by external contract calls through the RETURN and REVERT 
can be read by the calling contract with RETURNDATASIZE and RETURNDATACOPY.

gas costs
fixed cost + price of gas units
opcodes have their own gas cost, static + dynamic factors
Each transaction has an intrinsic cost of 21000 gas
Creating a contract costs another 32000 gas 
calldata costs 4 gas per empty (0) byte or 16 gas for other values
paid from the transaction before any opcode or transfer is executed

during execution, whole memory is accessible, but not for free
may trigger a memory expansion, which will cost gas


