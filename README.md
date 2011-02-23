Cash
====

Dead simple gem to work with Money/Currency without the hassle of Floats.

Usage
-----

    require 'cash'

    # Works with cents to avoid Floating point errors
    n = Cash.new(100)
    n.cents #=> 100
    n.to_s  #=> "1.00"
    n.to_f  #=> 1.0

    # Define currency as you see fit.
    a = Cash.new(100, :usd)
    b = Cash.new(100, :eur)
    a + b #=> Error! Cash::IncompatibleCurrency

    # Default is 100 cents in a dollar. Is your currency different, then just
    # tell it.
    n = Cash.new(100, cents_in_dollar: 5)
    n.cents #=> 100
    n.to_s  #=> "20.0"
    n.to_f  #=> 20.0

    n = Cash.new(100, cents_in_dollar: 10)
    n.cents #=> 100
    n.to_s  #=> "10.0"
    n.to_f  #=> 10.0

    n = Cash.new(100, cents_in_dollar: 1)
    n.cents #=> 100
    n.to_s  #=> "100"
    n.to_f  #=> 100.0

    # The default rounding method when dealing with fraction cents is
    # BigDecimal::ROUND_HALF_UP. Would you rather use bankers rounding, just
    # pass it as an argument.
    n = Cash.new(2.5)
    n.cents #=> 3

    n = Cash.new(2.5, rounding_method: BigDecimal::ROUND_HALF_EVEN)
    n.cents #=> 2