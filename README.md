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
        
    21. Index event fields make the field more quickly accessible to off-chain tools that parse events. However, note that each index field costs extra gas
        during emission, so it's not necessarily best to index the maximum allowed per event (three fields). Each event should use three indexed fields if
        ther are three or more fields, and gas usage is not particularly of concern for the events in question. If there are fewer than three fields, all of
        the fields should be indexed.
        
    22. Using bools for storage incurs overhead
        Use uint256(1) and uint256(2) for true/false to avoid a Gwarmaccess (100 gas), and to avoid Gsset (20000 gas) when changing from ‘false’ to ‘true’,
        after having been ‘true’ in the past. 
        https://github.com/OpenZeppelin/openzeppelin-contracts/blob/58f635312aa21f947cae5f8578638a85aa2519f5/contracts/security/ReentrancyGuard.sol#L23-L27
     
    23. FUNCTIONS GUARANTEED TO REVERT WHEN CALLED BY NORMAL USERS CAN BE MARKED PAYABLE
    
        if a function modifier such as onlyOwner is used, the function will revert if a normal user tries to pay the function. Marking the function as
        payable will lower the gas cost for legitimate callers because the compiler will not include checks for whether a payment was provided.
        
        function setOwner(address newOwner) public virtual onlyOwner {
        function withdraw(address to, uint256[] calldata ids) external onlyOwner {
        
    24. ADD REQUIRE() FOR ASSET ADDRESS CHECKS BEFORE DOING THE EXCHANGE 
        address should be verified (0x0) in oder to prevent wasting gas before every transactions. 
        
    25. STATE VARIABLES SHOULD BE CACHED IN STACK VARIABLES RATHER THAN RE-READING THEM FROM STORAGE
    
    26. USE A MORE RECENT VERSION OF SOLIDITY
        Use a solidity version of at least 0.8.0 to get overflow protection without SafeMath
        Use a solidity version of at least 0.8.2 to get compiler automatic inlining
        Use a solidity version of at least 0.8.3 to get better struct packing and cheaper multiple storage reads
        Use a solidity version of at least 0.8.4 to get custom errors, which are cheaper at deployment than revert()/require() strings
        Use a solidity version of at least 0.8.10 to have external calls skip contract existence checks if the external call has a return value
        
    27. USING STORAGE INSTEAD OF MEMORY FOR STRUCTS/ARRAYS SAVES GAS
    
    28. USAGE OF UINTS/INTS SMALLER THAN 32 BYTES (256 BITS) INCURS OVERHEAD
        When using elements that are smaller than 32 bytes, your contract’s gas usage may be higher. This is because the EVM operates on 32 bytes at a time.
        Therefore, if the element is smaller than that, the EVM must use more operations in order to reduce the size of the element from 32 bytes to the
        desired size.
        
    29. USING PRIVATE RATHER THAN PUBLIC FOR CONSTANTS, SAVES GAS
    
    30. EMPTY BLOCKS SHOULD BE REMOVED OR EMIT SOMETHING 
        eg : receive() external payable {}
        
    31. DON’T USE SAFEMATH ONCE THE SOLIDITY VERSION IS 0.8.0 OR GREATER
        Version 0.8.0 introduces internal overflow checks, so using SafeMath is redundant and adds overhead
        import { SafeMath } from  "@openzeppelin/contracts/utils/math/SafeMath.sol";
        
   32. Use assembly to check for address(0)
        if (nodeID == address(0)) {
        enabled = (addr != address(0)) && getBool(keccak256(abi.encodePacked("multisig.item", index, ".enabled")));
        
    33. array[index] += amount is cheaper than array[index] = array[index] + amount (or related variants)
        When updating a value in an array with arithmetic, using array[index] += amount is cheaper than array[index] = array[index] + amount. This is because
        you avoid an additonal mload when the array is stored in memory, and an sload when the array is stored in storage. This can be applied for any
        arithmetic operation including +=, -=,/=,*=,^=,&=, %=, <<=,>>=, and >>>=. This optimization can be particularly significant if the pattern occurs
        during a loop.
        
        avaxBalances[contractName] = avaxBalances[contractName] + msg.value;

        avaxBalances[contractName] = avaxBalances[contractName] - amount;
        
        
        
        
         
         

