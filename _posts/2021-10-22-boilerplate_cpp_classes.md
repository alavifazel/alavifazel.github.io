---
layout: post
title:  "Boilerplate C++ classes"
permalink: boilerplate-cpp-classes
description: A few boilerplate C++ classes that is useful for Electrical Engineering software projects
date:   2021-10-22 05:19:46 +0330
categories: ee
---

# Table of Contents
1. [Representing electrical signals in software](#representing-electrical-signals-in-software)

<a id="root-mean-square"></a>

# Representing electrical signals in software

Before continuing with the more advanced EE concepts, let's implement
the ideas we discussed so far in form of a software package. We would
therefore use these implementations readily in the future articles and
projects as well. We use the C++ language to write these constructs
since it is widely used in microcontroller and system programming; And
also supports advanced language features and paradigms.

One of the fundamental concepts that we would want to implement, is a
construct that would represent an *electrical signal* in our programs.
This idea can be implemented conveniently with OOP paradigm; i.e.
if we have a *class* that represents the type of a signal in our
program, instantiating it with:

{% highlight c++ %}
Signal s(<function_body>);
{% endhighlight %}

Would capture the signal's function, and with the appropriate definition
of our class this instance $$s$$ would readily contain all the frequently
used operations such as calculating its $$rms$$ and etc. Hence:

{% highlight c++ %}
s.getRms()
{% endhighlight %}

Would return the function's *rms* or:

{% highlight c++ %}
s.fourierTransform()
{% endhighlight %}

Would apply Fourier transform on our signal (an important math operation
that we will discuss in later articles) and so on.

Let's start by defining the base class:

{% highlight c++ %}
#include <cmath>
#include <functional>
class Signal {
    protected:
        using rftype =  std::function<double(double)>;
        rftype function;
    public:
        Signal(rftype f): function(f) {}
        double output(double x) { return function(x); }
        rftype getFunction() {return function; }
};
{% endhighlight %}

This class can be used as:

{% highlight c++ %}
Signal s([](double t) {return t*t;});
std::cout << s.output(3) << '\n';
std::cout << s.output(0.4) << '\n';
{% endhighlight %}

Running the program we get:

{% highlight c++ %}
9
0.16
{% endhighlight %}

As we see, the object $$s$$ can now represents a signal in our program.
For now, writing $$s.output(x)$$ gives the signal's output at time $$x$$ and
$$s.getFunction()$$ returns the signal's function definition if we needed
somewhere in our program.

Few remarks here:

1.  We included the header **functional** to make the type *std::function*

available in our program. With this type we captured the function's body
in the constructor.

2.  We defined a type alias for a real-valued math function that have

real-valued inputs and outputs $$(\Re\rightarrow\Re$$). We called this
alias **rftype** for **real-valued function type**.

3.  We declared the member variable $$function$$, as a protected member

because later on we want to derive more specific types of signal namely
DC, AC and Sinusoidal AC from this class.

Now let's move on to defining derived classes. The first one is for the
DC signals which has a straightforward definition.

{% highlight c++ %}
class DcSignal: public Signal {
    public:
        DcSignal(double dcValue): Signal([dcValue](double t) -> double {
            return dcValue;
        }){}
};
{% endhighlight %}

It can be used as:

{% highlight c++ %}
DcSignal s(4);
{% endhighlight %}

For AC signal class:

{% highlight c++ %}
class AcSignal: public Signal {
    public:
        AcSignal(rftype func, double p): Signal([func,p](double t) -> double {
            if(std::abs(t) <= std::abs(p)) return func(t);
            else return func(t - (int)(t/p) * p);
        }), f(1/p), p(p){}

        double getRms() {
            return std::sqrt(1/p * numerical_integration(function, 0, p));
        }

        double getFrequency() { return f; }
        double getPeriod() { return p; }
    protected:
        double f, p;
};
{% endhighlight %}

This class is also straightforward. It's constructor accepts a function
and period in which the function would repeat after that point. Note
that in $$getRms$$ we uses *numerical integration* for estimating the
definite integral. This function can be implemented in various ways. A
quick one is to use the trapezoidal method:

{% highlight c++ %}
double numerical_integration(std::function<double(double)> f,
                        double a, double b, double N = 10000) {
    double h = (b - a) / N;
    double tmp = 0;
    tmp += f(a);
    tmp += f(b);
    while(a < b) {
        tmp += 2 * f(a);
        a += h;
    }
    return (h/2)*tmp;
}
{% endhighlight %}

Example usage of *AcSignal*:

{% highlight c++ %}
AcSignal s([](double t) {return t*t;}, 2);
cout << s.output(0.5) << '\n';
cout << s.output(2.5) << '\n';
{% endhighlight %}

Produces:

    0.25
    0.25

Now let's define a class that we'd likely use the most: Sinusoidal
signals. Since this class is a type of AC signal and it's periodic, we
derive it from the *AcSignal*.

{% highlight c++ %}
class SinusoidalAcSignal: public AcSignal {
    public:
        SinusoidalAcSignal(double amplitude, double frequency,
                            double phase = 0):
            AcSignal([amplitude, frequency, phase](double t) -> double {
            return amplitude * std::sin(t*2*3.14159268*frequency + phase);
        }, 1/frequency), a(amplitude) {}

        double getRms() { return a/std::sqrt(2); }
        double getAmplitude() { return a; }
    private:
        double a;
};
{% endhighlight %}

(The definition of these classes are presented in a single file inside
this article's directory.)

We have now defined some boilerplate classes that we'd use in situations
such as when we want to generate some sinusoidal signal for an output
pin of a microcontroller. For another example when we want to simulate
	an input signal for analyzing circuits with a softwar
