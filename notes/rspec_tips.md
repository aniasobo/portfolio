# Rspec tips

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

**Using let**

Oystercard example from walkthrough:

```
let(:journey){ {entry_station: entry_station, exit_station: exit_station} }

it 'stores a journey' do
  subject.touch_in(entry_station)
  subject.touch_out(exit_station)
  expect(subject.journeys).to include journey
end
```

- correct double syntax for using a double with mock methods and method responses:

```
journey_class_double = double :journey, complete: true, fare: 1
```





### To use SimpleCov

1. install in Gemfile, bundle etc
2. in spec_helper, paste this ABOVE RSpec.configure block:   

```
SimpleCov.formatter = SimpleCov::Formatter::MultiFormatter.new([
  SimpleCov::Formatter::Console,
  # Want a nice code coverage website? Uncomment this next line!
  # SimpleCov::Formatter::HTMLFormatter
])
SimpleCov.start
```

3. require 'spec_helper' in your spec files
4. run rspec  
    