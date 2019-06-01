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
