# bitcoin-minor-using-python

from hashlib import sha256

MAX_NONCE = 100000000000

def SHA256(text):

   return sha256(text.encode("ascii")).hexdigest()

def mine(block_number,transaction,previous_hash,prefix_zeros):
    
    prefix_str='0'*prefix_zeros
    for nonce in range(MAX_NONCE):
    
        text=str(block_number)+transaction+previous_hash+str(nonce)
        new_hash=SHA256(text)
       
        if new_hash.startswith(prefix_str):
            
           print(f"hey! successfully mined bitcoins with nonce value:{nonce}")
           return new_hash
    
    raise BaseException(f"couldn't find correct has after trying {MAX_NONCE} times")

if __name__=='__main__':

    transaction='''
    raj->ram->20,  #this bitcoin value can be different
    aman->vipin->15
    '''
    difficulty=6
    import time
    start=time.time()
    print("start mining")

    new_hash=mine(5,transaction,"0000000xa591a6d40bf420404a011733cfb7b190d62c65bf0bcda32b57b277d9ad9f146e",difficulty)
    total_time=str((time.time()-start))
    print(f"end mining.mining took:{total_time} seconds")
    print(new_hash)
        
