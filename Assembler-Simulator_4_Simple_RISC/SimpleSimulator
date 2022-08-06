import sys
import matplotlib.pyplot as plt

# ******************************************************************************************************************
# INPUT*************************************************************************************************************
# ******************************************************************************************************************


l=[]                
for line in sys.stdin:
    l.append(line.strip())


# ******************************************************************************************************************
# Functions(x20)****************************************************************************************************
# ******************************************************************************************************************


def decimalTobinary_8bits(n):
    n_bin=''
    n=int(n)
    while n>0:
        d=n%2
        n=n//2
        n_bin+=str(d)
    n_bin=n_bin[-1::-1]
    zero_left=8-len(n_bin)
    n_bin=('0'*zero_left)+n_bin
    return n_bin

def decimalTobinary_16bits(n):
    n_bin=''
    n=int(n)
    while n>0:
        d=n%2
        n=n//2
        n_bin+=str(d)
    n_bin=n_bin[-1::-1]
    zero_left=16-len(n_bin)
    n_bin=('0'*zero_left)+n_bin
    return n_bin

def binaryTodecimal(st):
    n_dec=0
    st=st[-1::-1]
    for i in range(0,len(st)):
        a=int(st[i])
        n_dec+=a*2**i
    return n_dec


# Here what the plan i propose is that we will make 29 functions for each instruction of type A, B, C, D, E.
# And whatever happens in the execution loop uske accordinly yeh functions call karenge using first 5 index values which is OPcode
# and perform the changes in register PC and variable values as asked in the question

def addition(line):
    flag=0
    reg_value[reg_addr[line[6:]]]=reg_value[reg_addr[line[0:3]]]+reg_value[reg_addr[line[3:6]]]

    # CHECKING FOR OVERFLOW AND UNDERFLOW (V=1)

    if reg_value[reg_addr[line[6:]]]<(2**16) and reg_value[reg_addr[line[6:]]]>=0:
        pc_line[reg_index[reg_addr[line[6:]]]]=decimalTobinary_16bits(reg_value[reg_addr[line[6:]]])

    else:
        flag=1
        if reg_value[reg_addr[line[6:]]]>=(2**16): # OVERFLOW
            reg_value[reg_addr[line[6:]]]=(reg_value[reg_addr[line[6:]]])%(2**16)
            pc_line[reg_index[reg_addr[line[6:]]]]=decimalTobinary_16bits(reg_value[reg_addr[line[6:]]])
            reg_value['FLAGS']=8 # SETTING 'V' BIT = 1
            pc_line[reg_index['FLAGS']]=decimalTobinary_16bits(reg_value['FLAGS'])

        else: # UNDERFLOW
            reg_value[reg_addr[line[6:]]]=0
            pc_line[reg_index[reg_addr[line[6:]]]]=decimalTobinary_16bits(reg_value[reg_addr[line[6:]]])
            reg_value['FLAGS']=8 # SETTING V BIT = 1
            pc_line[reg_index['FLAGS']]=decimalTobinary_16bits(reg_value['FLAGS'])

    if flag==0:
        reg_value['FLAGS']=0
        pc_line[reg_index['FLAGS']]='0000000000000000'

def subtraction(line):
    flag=0
    reg_value[reg_addr[line[6:]]]=reg_value[reg_addr[line[0:3]]]-reg_value[reg_addr[line[3:6]]]

    # CHECKING FOR OVERFLOW AND UNDERFLOW (V=1)

    if reg_value[reg_addr[line[6:]]]<(2**16) and reg_value[reg_addr[line[6:]]]>=0:
        pc_line[reg_index[reg_addr[line[6:]]]]=decimalTobinary_16bits(reg_value[reg_addr[line[6:]]])

    else:
        flag=1
        if reg_value[reg_addr[line[6:]]]>=(2**16): # OVERFLOW
            reg_value[reg_addr[line[6:]]]=(reg_value[reg_addr[line[6:]]])%(2**16)
            pc_line[reg_index[reg_addr[line[6:]]]]=decimalTobinary_16bits(reg_value[reg_addr[line[6:]]])
            reg_value['FLAGS']=8 # SETTING 'V' BIT = 1
            pc_line[reg_index['FLAGS']]=decimalTobinary_16bits(reg_value['FLAGS'])

        else: # UNDERFLOW
            reg_value[reg_addr[line[6:]]]=0
            pc_line[reg_index[reg_addr[line[6:]]]]=decimalTobinary_16bits(reg_value[reg_addr[line[6:]]])
            reg_value['FLAGS']=8 # SETTING V BIT = 1
            pc_line[reg_index['FLAGS']]=decimalTobinary_16bits(reg_value['FLAGS'])

    if flag==0:
        reg_value['FLAGS']=0
        pc_line[reg_index['FLAGS']]='0000000000000000'

def multiplication(line):
    flag=0
    reg_value[reg_addr[line[6:]]]=reg_value[reg_addr[line[0:3]]]*reg_value[reg_addr[line[3:6]]]

    # CHECKING FOR OVERFLOW AND UNDERFLOW (V=1)

    if reg_value[reg_addr[line[6:]]]<(2**16) and reg_value[reg_addr[line[6:]]]>=0:
        pc_line[reg_index[reg_addr[line[6:]]]]=decimalTobinary_16bits(reg_value[reg_addr[line[6:]]])

    else:
        flag=1
        if reg_value[reg_addr[line[6:]]]>=(2**16): # OVERFLOW
            print(reg_value[reg_addr[line[6:]]])
            reg_value[reg_addr[line[6:]]]=(reg_value[reg_addr[line[6:]]])%(65536)
            print(reg_value[reg_addr[line[6:]]])
            pc_line[reg_index[reg_addr[line[6:]]]]=decimalTobinary_16bits(reg_value[reg_addr[line[6:]]])
            reg_value['FLAGS']=8 # SETTING 'V' BIT = 1
            pc_line[reg_index['FLAGS']]=decimalTobinary_16bits(reg_value['FLAGS'])

        else: # UNDERFLOW
            reg_value[reg_addr[line[6:]]]=0
            pc_line[reg_index[reg_addr[line[6:]]]]=decimalTobinary_16bits(reg_value[reg_addr[line[6:]]])
            reg_value['FLAGS']=8 # SETTING V BIT = 1
            pc_line[reg_index['FLAGS']]=decimalTobinary_16bits(reg_value['FLAGS'])

    if flag==0:
        reg_value['FLAGS']=0
        pc_line[reg_index['FLAGS']]='0000000000000000'

def move_immediate(line):
    reg_value[reg_addr[line[0:3]]]=binaryTodecimal(line[3:])
    pc_line[reg_index[reg_addr[line[0:3]]]]=decimalTobinary_16bits(reg_value[reg_addr[line[0:3]]])
    reg_value['FLAGS']=0
    pc_line[reg_index['FLAGS']]='0000000000000000'

def move_register(line): # mov r1 r2 we give r2 = r1
    reg_value[reg_addr[line[3:]]]=reg_value[reg_addr[line[0:3]]]
    pc_line[reg_index[reg_addr[line[3:]]]]=decimalTobinary_16bits(reg_value[reg_addr[line[3:]]])
    reg_value['FLAGS']=0
    pc_line[reg_index['FLAGS']]='0000000000000000'

def load(line):
    index=binaryTodecimal(line[3:]) # mem_addr is index of the var in the memory list
    reg_value[reg_addr[line[0:3]]]=binaryTodecimal(l_memory[index]) # the value at that index is to be stored in register
    pc_line[reg_index[reg_addr[line[0:3]]]]=decimalTobinary_16bits(reg_value[reg_addr[line[0:3]]])
    reg_value['FLAGS']=0
    pc_line[reg_index['FLAGS']]='0000000000000000'
    x_axis.append(cycle)
    y_axis.append(line[3:])

def store(line):
    value_var=reg_value[reg_addr[line[0:3]]] # extract the value of register
    index=binaryTodecimal(line[3:]) # mem_addr is index of the var in the memory list
    l_memory[index]=decimalTobinary_16bits(value_var) # store the value at the index pointed by mem_addr
    reg_value['FLAGS']=0
    pc_line[reg_index['FLAGS']]='0000000000000000'
    x_axis.append(cycle)
    y_axis.append(line[3:])

def divide(line): # div r3 r4 means R0=quo(r3/r4) and R1=rem(r3/r4)
    reg_value['R0']=int((reg_value[reg_addr[line[0:3]]])/(reg_value[reg_addr[line[3:]]]))
    reg_value['R1']=reg_value[reg_addr[line[0:3]]]-(reg_value['R0']*(reg_value[reg_addr[line[3:]]]))
    pc_line[reg_index['R0']]=decimalTobinary_16bits(reg_value['R0'])
    pc_line[reg_index['R1']]=decimalTobinary_16bits(reg_value['R1'])
    reg_value['FLAGS']=0
    pc_line[reg_index['FLAGS']]='0000000000000000'

def compare(line):
    val_1=reg_value[reg_addr[line[0:3]]]
    val_2=reg_value[reg_addr[line[3:]]]
    if val_1>val_2:
        reg_value['FLAGS']=2
    elif val_1<val_2:
        reg_value['FLAGS']=4
    else:
        reg_value['FLAGS']=1
    pc_line[reg_index['FLAGS']]=decimalTobinary_16bits(reg_value['FLAGS'])

def unconditional_jump(line):
    index=binaryTodecimal(line[0:])
    pc_line[0]=decimalTobinary_8bits(i)
    reg_value['FLAGS']=0
    pc_line[reg_index['FLAGS']]='0000000000000000'
    x_axis.append(cycle)
    y_axis.append(line[0:])
    return index

def less_than_jump(line):
    index=binaryTodecimal(line[0:])
    if reg_value['FLAGS']==4:
        pc_line[0]=decimalTobinary_8bits(i)
        reg_value['FLAGS']=0
        pc_line[reg_index['FLAGS']]='0000000000000000'
        x_axis.append(cycle)
        y_axis.append(line[0:])  
        return index
    else:
        reg_value['FLAGS']=0
        pc_line[reg_index['FLAGS']]='0000000000000000'
        return -1

def greater_than_jump(line):
    index=binaryTodecimal(line[0:])
    if reg_value['FLAGS']==2:
        pc_line[0]=decimalTobinary_8bits(i)
        reg_value['FLAGS']=0
        pc_line[reg_index['FLAGS']]='0000000000000000'
        x_axis.append(cycle)
        y_axis.append(line[0:])
        return index
    else:
        reg_value['FLAGS']=0
        pc_line[reg_index['FLAGS']]='0000000000000000'
        return -1

def equal_jump(line):
    index=binaryTodecimal(line[0:])
    if reg_value['FLAGS']==1:
        pc_line[0]=decimalTobinary_8bits(i)
        reg_value['FLAGS']=0
        pc_line[reg_index['FLAGS']]='0000000000000000'
        x_axis.append(cycle)
        y_axis.append(line[0:])
        return index
    else:
        reg_value['FLAGS']=0
        pc_line[reg_index['FLAGS']]='0000000000000000'
        return -1

def right_shift(line):
    imm_shift=binaryTodecimal(line[3:])
    reg_value[reg_addr[line[0:3]]]/=(2**imm_shift)
    pc_line[reg_index[reg_addr[line[0:3]]]]=decimalTobinary_16bits(reg_value[reg_addr[line[0:3]]])
    reg_value['FLAGS']=0
    pc_line[reg_index['FLAGS']]='0000000000000000'

def left_shift(line):
    imm_shift=binaryTodecimal(line[3:])
    reg_value[reg_addr[line[0:3]]]*=(2**imm_shift)
    pc_line[reg_index[reg_addr[line[0:3]]]]=decimalTobinary_16bits(reg_value[reg_addr[line[0:3]]])
    reg_value['FLAGS']=0
    pc_line[reg_index['FLAGS']]='0000000000000000'

def exclusive_xor(line):
    s=''
    s_1=pc_line[reg_index[reg_addr[line[0:3]]]]
    s_2=pc_line[reg_index[reg_addr[line[3:6]]]]
    for i in range(len(s_1)):
        s+=str(int(s_1[i])^int(s_2[i]))
    pc_line[reg_index[reg_addr[line[6:]]]]=s
    reg_value[reg_addr[line[6:]]]=binaryTodecimal(s)
    reg_value['FLAGS']=0
    pc_line[reg_index['FLAGS']]='0000000000000000'

def or_operation(line):
    s=''
    s_1=pc_line[reg_index[reg_addr[line[0:3]]]]
    s_2=pc_line[reg_index[reg_addr[line[3:6]]]]
    for i in range(len(s_1)):
        s+=str(int(s_1[i])|int(s_2[i]))
    pc_line[reg_index[reg_addr[line[6:]]]]=s
    reg_value[reg_addr[line[6:]]]=binaryTodecimal(s)
    reg_value['FLAGS']=0
    pc_line[reg_index['FLAGS']]='0000000000000000'

def and_operation(line):
    s=''
    s_1=pc_line[reg_index[reg_addr[line[0:3]]]]
    s_2=pc_line[reg_index[reg_addr[line[3:6]]]]
    for i in range(len(s_1)):
        s+=str(int(s_1[i])&int(s_2[i]))
    pc_line[reg_index[reg_addr[line[6:]]]]=s
    reg_value[reg_addr[line[6:]]]=binaryTodecimal(s)
    reg_value['FLAGS']=0
    pc_line[reg_index['FLAGS']]='0000000000000000'

def not_operation(line):
    s=''
    s_1=pc_line[reg_index[reg_addr[line[0:3]]]]
    for i in range(len(s_1)):
        s+=str(int(not int(s_1[i])))
    pc_line[reg_index[reg_addr[line[3:]]]]=s
    reg_value[reg_addr[line[3:]]]=binaryTodecimal(s)
    reg_value['FLAGS']=0
    pc_line[reg_index['FLAGS']]='0000000000000000'


# While Traversing through the input machine code we'll use while loop instead of FOR loop************************

i=0 # VALUE OF PROGRAM COUNTER

# IT IS A LIST CONSISTING OF [PC(0),R0(1),R1(2),R2(3),R3(4),R4(5),R5(6),R6(7),FLAGS(8)] LISTS PRINTED AFTER EACH INSTRUCTION
pc_line=['00000000','0000000000000000','0000000000000000','0000000000000000','0000000000000000','0000000000000000','0000000000000000','0000000000000000','0000000000000000']

reg_addr={'000':'R0','001':'R1','010':'R2','011':'R3','100':'R4','101':'R5','110':'R6','111':'FLAGS'}
reg_value={'R0':0,'R1':0,'R2':0,'R3':0,'R4':0,'R5':0,'R6':0,'FLAGS':0}
reg_index={'R0':1,'R1':2,'R2':3,'R3':4,'R4':5,'R5':6,'R6':7,'FLAGS':8}

l_memory=[] # IT IS A LIST WHICH REPRESENTS 256 LINES OF MEMORY

s='0000000000000000' # 16 BIT MEMORY

x_axis=[]
cycle=0

y_axis=[]

# ******************************************************************************************************************
# FORMING MEMORY 512 BYTE DOUBLE ADDRESSABLE MEMORY (256 LINES)*****************************************************


for j in range(256):
    if j<len(l):
        l_memory.append(l[j])
    else:
        l_memory.append(s)


# *************************************************************************************************************
# FORMING L_OUTPUT LIST*****************************************************************************************

# Here what we are doing is we will traverse through the input list l, and perform the required operations as per the machine code
# REASON FOR USING WHILE LOOP OVER FOR LOOP: We might encounter the jmp instructions, in those cases we require
# to jump to some previous index of input list l to access that particular machine code as asked by the jump instruction
# The loop ends when i has reached len(l)-1 which is going to be halt instruction and after that we print the memory

while(i<len(l)):

    x_axis.append(cycle)
    y_axis.append(pc_line[0])

    opcode=l[i][0:5] # EXTRACTING OPCODE AND THEN PERFORMING THE OPERATION

    if(opcode=='10000'):
        addition(l[i][7:]) # 0 1 2 3 4 for opcode and 5 6 unused
        pc_line[0]=decimalTobinary_8bits(i)
        print(*pc_line)
        i+=1

    elif opcode=='10001':
        subtraction(l[i][7:]) # 0 1 2 3 4 for opcode and 5 6 unused
        pc_line[0]=decimalTobinary_8bits(i)
        print(*pc_line)
        i+=1

    elif opcode=='10110':
        multiplication(l[i][7:]) # 0 1 2 3 4 for opcode and 5 6 unused
        pc_line[0]=decimalTobinary_8bits(i)
        print(*pc_line)
        i+=1
        
    elif opcode=='10010':
        move_immediate(l[i][5:]) # 0 1 2 3 4 for opcode
        pc_line[0]=decimalTobinary_8bits(i)
        print(*pc_line)
        i+=1

    elif opcode=='10011':
        move_register(l[i][10:]) # 0 1 2 3 4 for opcode and 5 6 7 8 9 unused
        pc_line[0]=decimalTobinary_8bits(i)
        print(*pc_line)
        i+=1

    elif opcode=='10100':
        load(l[i][5:]) # 0 1 2 3 4 for opcode ; 5 6 7 reg addr; 8 - 15 mem_addr (TYPE D)
        pc_line[0]=decimalTobinary_8bits(i)
        print(*pc_line)
        i+=1

    elif opcode=='10101':
        store(l[i][5:]) # type D
        pc_line[0]=decimalTobinary_8bits(i)
        print(*pc_line)
        i+=1

    elif opcode=='10111':
        divide(l[i][10:]) # type C
        pc_line[0]=decimalTobinary_8bits(i)
        print(*pc_line)
        i+=1

    elif opcode=='11000':
        right_shift(l[i][5:]) # type B
        pc_line[0]=decimalTobinary_8bits(i)
        print(*pc_line)
        i+=1

    elif opcode=='11001':
        left_shift(l[i][5:]) # type B
        pc_line[0]=decimalTobinary_8bits(i)
        print(*pc_line)
        i+=1

    elif opcode=='11010':
        exclusive_xor(l[i][7:]) # type A
        pc_line[0]=decimalTobinary_8bits(i)
        print(*pc_line)
        i+=1

    elif opcode=='11011':
        or_operation(l[i][7:]) # type A
        pc_line[0]=decimalTobinary_8bits(i)
        print(*pc_line)
        i+=1

    elif opcode=='11100':
        and_operation(l[i][7:]) # type A
        pc_line[0]=decimalTobinary_8bits(i)
        print(*pc_line)
        i+=1

    elif opcode=='11101':
        not_operation(l[i][10:]) # type C
        pc_line[0]=decimalTobinary_8bits(i)
        print(*pc_line)
        i+=1

    elif opcode=='11110':
        compare(l[i][10:]) # type c
        pc_line[0]=decimalTobinary_8bits(i)
        print(*pc_line)
        i+=1

    elif opcode=='11111':
        pc_line[0]=decimalTobinary_8bits(i)
        print(*pc_line)
        i=unconditional_jump(l[i][8:]) #type E

    elif opcode=='01100':
        i_shift=less_than_jump(l[i][8:]) #type E
        pc_line[0]=decimalTobinary_8bits(i)
        print(*pc_line)
        if i_shift==-1:
            i+=1
        else:
            i=i_shift
        

    elif opcode=='01101':
        i_shift=greater_than_jump(l[i][8:]) #type E
        pc_line[0]=decimalTobinary_8bits(i)
        print(*pc_line)
        if i_shift==-1:
            i+=1
        else:
            i=i_shift

    elif opcode=='01111':
        i_shift=equal_jump(l[i][8:]) #type E
        pc_line[0]=decimalTobinary_8bits(i)
        print(*pc_line)
        if i_shift==-1:
            i+=1
        else:
            i=i_shift

    elif opcode=='01010':
        reg_value['FLAGS']=0
        pc_line[reg_index['FLAGS']]='0000000000000000'
        pc_line[0]=decimalTobinary_8bits(i)
        print(*pc_line)
        break

    cycle+=1

for i in l_memory:
    print(i)


# SCATTER PLOT X--> CYCLE NUMBER AND Y-->MEMORY INSTRUCTION BEING ACCESSED

plt.scatter(x_axis,y_axis,c="red")
plt.show()








        








        



