# Smart-Contract-Gas-Optimization

## Here comment les gas consuption as given below.

    1. ++x <  x++ or  x=x+1

    2. For state variables 
    x = x + 10  < x +=10 

    3. If there is a constant variable on the program 
    uint public constant  x = 10 < uint public x = 10 
    
    4. Number of loop itereations need to less. Otherwise it use more gas if with iterations
    
    5. Require , revert , assert error message need to be set with less characters.


