# Week three 10-16.06.2019

## Goals:

- [ ] Build a simple web app
- [ ] Follow an effective debugging process for web applications
- [ ] Explain the basics of how the web works (e.g. request/response, HTTP, HTML, CSS)
- [ ] Explain the MVC pattern

---  

## Practice:

Date | Project | progress
--- | --- | ---
10.06 | Battle - pairing | feedback

---

### Notes on the weekend challenge/code review:

The correct way to stub the Twilio calling method:

```
describe Takeaway
  subject(:takeaway) { described_class.new }

  before do
    allow(takeaway).to receive(:send_text)
  end

  it 'sends a payment confirmation text message' do
    expect(takeaway).to receive(:send_text).with("Thank you for your order: £20.93")
    takeaway.complete_order(20.93)
  end
end
```

[other options:](https://github.com/makersacademy/course/blob/master/pills/levels_of_stubbing.md)

1. Stub Class in Your Application (code above)
2. Stub the Gem Associated with 3rd Party API
3. Stub the Network with Webmock
4. Manage Your Network Stubbing with VCR

---

## Servers 1 practical:


### Code review workshop notes:

- private methods are not to be tested!
- be careful to not expose instance vars by assigning them as attribute accessors instead of readers
- dotenv gem: create .env files for your environment variables (as alternative to storing them in bash_profile), remember to add all .env files to .gitignore 
- zsh? alt to Terminal
- integration test vs feature test - the former is concerned primarily with testing the relationships between objects/classes, the latter tests those naturally in the course of testing the app


### The two schools of TDD

[London school vs Chicago school of TDD](http://programmers.stackexchange.com/questions/123627/what-are-the-london-and-chicago-schools-of-tdd)

```
# London Style
describe Order do
  let(:menu) { double :menu, price: '£1.00', contains?: true }
  subject(:order) { described_class.new(menu) }

  it 'order total to be sum of items added' do
    order.add('Pizza')
    order.add('Pizza')
    expect(order.total).to eq '£2.00'
  end
end
```

```
# Chicago Style --> arguably an 'integration' or 'feature' test
describe Order do
  subject(:order) { described_class.new(Menu.new) } # note real Menu class

  it 'order total to be sum of items added' do
    order.add('Pizza')
    order.add('Pizza')
    expect(order.total).to eq '£2.00'
  end
end
```
