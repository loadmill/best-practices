# Notes
## First request 'Loop until condition is true'
- The parameter `number_for_fc_example` is initialized as 0 in the global parameters section. Thus, every change of this param affects its value in all other requests as it's a flow scope parameter.
- Once a condition is set in the Flow Control panel, at the end of every request (after the postscript and after the extractions), the condition will be checked and as long as the condition is not true OR the number of iterations hasn't reached the `max iter.`, it'll keep going.

## About "skip"
- It is important to remember that **a skip condition does not interrupts the request where it is defined**. i.e if your skip condition is `is_num_bigger_than_10`, and the same request also loops over `num` from 1 to 20 adding 1 every iteration, the next request will be skipped indeed but also the loop will continue until `num = 20`. 

## About "stop"
- **Like 'skip' condition, the request it is defined in, will still be completed, and only then the flow will be stopped**. In this flow a loop is included in the stop condition request to show that even though the stop condition (`is_num_equals_8`) was true in one of the iterations, (reminder: the loop increases `num` by 1 every iteration), the loop kept going untill `number_for_fc_flow` was equal to 10.