# Smart-Contract-Gas-Optimization

##  Less gas consuption as given below.

    1. ++x <  x++ or  x=x+1

    2. For state variables 
    x = x + 10  < x +=10 

    3. If there is a constant variable on the program 
    uint public constant  x = 10 < uint public x = 10 
    
    4. Number of loop itereations need to less. Otherwise it use more gas if with iterations
    
    5. Require , revert , assert error message need to be set with less characters.
    
    6. Custom errors are more gas efficient than using require with a string explanation. 
        So ideally you'd always use this over require.
    7. Compared to regular state variables, the gas costs of constant and immutable variables are much lower
    
    8. constant values can sometimes be cheaper than immutable values.
    
    9. Using calldata instead of memory for read-only arguments in external functions saves gas
    
    10. Nice atricle about unchecked block https://ethereum.stackexchange.com/questions/113221/what-is-the-purpose-of-unchecked-in-solidity
    
    11.  ADD UNCHECKED {} FOR SUBTRACTIONS WHERE THE OPERANDS CANNOT UNDERFLOW BECAUSE OF A PREVIOUS REQUIRE() OR IF-STATEMENT.
    
    12. ++I/I++ SHOULD BE UNCHECKED{++I}/UNCHECKED{I++} WHEN IT IS NOT POSSIBLE FOR THEM TO OVERFLOW, AS IS THE CASE WHEN USED IN FOR- AND WHILE-LOOPS.
    
    13. Function name optimization :
    
        https://medium.com/joyso/solidity-how-does-function-name-affect-gas-consumption-in-smart-contract-47d270d8ac92
    
    14. SPLITTING REQUIRE() STATEMENTS THAT USE && SAVES GAS
    
    15. DON’T COMPARE BOOLEAN EXPRESSIONS TO BOOLEAN LITERALS
        if (<x> == true) => if (<x>), if (<x> == false) => if (!<x>)
        
    16. USE CUSTOM ERRORS RATHER THAN REVERT()/REQUIRE() STRINGS TO SAVE GAS 
        https://ethereum.stackexchange.com/questions/101782/requirecondition-message-vs-revert-with-a-custom-error-which-is-better-a
        
    17. Don't initialize variables with default value .
        bool dataValidity = false;     for (uint256 i = 0; i < _assets.length; i++) {}
        
    
    18. Using private rather than public for constants, saves gas 
        bytes32 public constant UPDATER_ROLE = keccak256("UPDATER_ROLE");
        
    
    19.  Use != 0 instead of > 0 for unsigned integer comparison 
         require(_twap > 0, "NFTOracle: price should be more than 0");
         if (priceInfo.updatedAt > 0) {}
         
   20. Loop optimization 
       if your looping array get array length into cache.
       use UNCHECKED{++I} . 
       Read more..https://hackmd.io/@totomanov/gas-optimization-loops
         
         

