# merkle_tree
'''
    merkle_tree() function will return a hash value,which is the merkle root in the whole blockchain
'''
from hashlib import sha256 
#use the function hash_encrypt() and add_two_value() to find out the final hash value
def merkle_tree(list):
    while(len(list)>1):
        list=hash_encrypt(list)
        list=add_two_value(list)
    final=list.pop()
    return sha256(final.encode('utf-8')).hexdigest()
#turn every data inside the list into hash value
def hash_encrypt(list):
    hash_list=[]
    for data in list:
        hash_list.append(sha256(data.encode('utf-8')).hexdigest())
    return hash_list
#add two values together, if the total number is odd number, leave the last one behind
def add_two_value(list):
    child_list=[]
    if(len(list)%2==0):
        i=0
        while(i<len(list)-1):
            child_list.append(list[i]+list[i+1])
            i+=2
        return child_list
    elif(len(list)%2==1):
        i=0
        while(i<len(list)-2):
            child_list.append(list[i]+list[i+1])
            i+=2
        #the last one will copy itself then add itself
        temp=list.pop()
        child_list.append(temp+temp)
        return child_list
    else:
        print('The array is illegal')
