# Rspec tips from The Rspec Book

- add --format doc to view better error output, like this:

```
rspec spec/docking_station_spec.rb --format doc
```

- in the describe block, on second line, add this statement that will be executed before each example:

```
before(:each) do
# stuff
end
```

- alternatively to the before each block, use the let(:method){} like so:

```
describe 'stuff' do
let(:your_instance_var) { block of code to execute }
it do
end #blocks
end
```

- use ::Namespace operator before constants:

```
ClassName::CONSTANT_NAME.times do
#block
end
```

- the two main matchers to use: .to eq & {}.to raise_error
- doubles are empty containers so they must be allowed to receive a mock message from a mock method in order to be helpful -- be careful to not make your mock tests test themselves (i.e. sending mock messages to a double and then having that outcome be the thing under test)
- remove dependencies (object relying on another object's method in test) with mocks and doubles -- testing methods in isolation is ideal; objects being dependencies can be costly to instantiate but cheap to mock  

**pending tests:**  

```
describe "an example" do
  it "is implemented but waiting" do
    pending("something else getting finished")
    this_should_not_get_executed
  end
end
```

should return exit status 0, the output should contain "1 example, 0 failures, 1 pending" and output:

```
Pending:
  an example is implemented but waiting
    # something else getting finished
    # ./pending_without_block_spec.rb:2
```
    