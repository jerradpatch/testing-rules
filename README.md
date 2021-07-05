#Testing rules 
- a general set of rules that can be applied to any testing framework. See the 'WHY?' below for the need for this and reasoning.

### <b>File, folder, and test naming conventions and layout</b> 
- folder/file/describe/test structure and naming conventions for PRM

1) follow the folder naming convention for which file your function is what your creating test.
first group tests for a file then function then group common concepts into describe blocks (physical mimicking then concept grouping): ex

```jest
describe('login:actions', ()=>{ //folder 'login' and file 'actions' name -> physical groupings before concept
  describe('login', ()=>{ //function name -> physical groupings before concept
    describe('userName='mike', password=p' or 
             '<logical concept behind params meaning> 'userOver21',
            () => { //physical or concepts grouped to give the meaning of the params we are using
      describe('success', ()=>{ //concepts grouped
       //all tests for success scenarios
      describe('failure', ()=>{
       //all tests for failure scenarios: 500s 400s...
    });
  });
});
```

Note: describe block text should not contain long descriptions of concepts

2) when testing a file, all functions that the file is dependent on must also be tested. This mean following points 1 and 2, testing a single file can result in make files being created. Note, not all functions in the new 'dependent' files that are created need to be tested just the functions that the original file is dependent on. ex:
file 1A has function 2A. Function 2A  is dependent on function 2B in file 1B. In order to write tests for 2A, we need to prove that 2B works as expected, so we have to write tests for 2B to complete 2A testing.
Fixtures or Seeds - data that that is used when testing.

### <b>For large data structures used in mocking:</b>
1)   We should add these files to a series of folders the root of which called 'fixtures' which is located directly next to the file that we are testing. The folder structure to the file should follow the concept grouping used in the describe blocks of the test that the data structure belongs to.
Ex: fixtures -> userOver21 -> success.ts. 
Where the 'fixtures' folder is located next to the file we are testing 'actions.ts'.

2)   We should put each structure into its own file named after its logical usage. For example, an item response from the function can be very large, put this into its own file called be the data structures usage "success.ts".
note: the above will apply to both integration and unit tests going forward.

### <b>WHY?</b>
make sure we cover all the scenarios for tests and thus improve confidence in our deployments
allow others to find the scenarios that are covered for the function they are using, and thus reduce duplicate test scenarios or over testing. Also, this allows us to quickly find the scenario when we find a production issue.
