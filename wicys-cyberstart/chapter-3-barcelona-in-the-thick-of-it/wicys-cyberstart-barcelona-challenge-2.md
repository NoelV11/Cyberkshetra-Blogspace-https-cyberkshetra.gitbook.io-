# WiCYS CyberStart (Barcelona) Challenge 2

![](../../.gitbook/assets/CS.png)

## Briefing L03 C02 <a href="#fb88" id="fb88"></a>

### Maths at Light Speed <a href="#8cf9" id="8cf9"></a>

&#x20;                                            ![](https://miro.medium.com/max/756/1\*bwczYlj8WpC9OjiMGwIqDQ.jpeg)

> Intern, I hope you know how to use a calculator? Of course you do. So, in theory you should be able to bypass a security gateway to a warehouse we believe holds clues to the whereabouts of a gang we are in hot pursuit of. The thing is, the gateway was created by someone who loves doing everything super fast! That means you only get 0.1 seconds to answer the question asked by the gateway. Can you find a way around it?
>
> **Tip**: Bypass the calculator lock to get the flag.

We find this cool calculator when proceeding to the challenge.

&#x20;                                    ![](https://miro.medium.com/max/784/1\*n4tds2njp-c58IweJ7YepA.jpeg)

The downside is that it locks out the answer submission area before we can perform lightning-speed calculations, to answer the question.

Since the calculator is dynamic, it would be wise to see the source code working in action

This is how the Javascript looks before clicking on the ‘Spin for question’ button

&#x20;                                          ![](https://miro.medium.com/max/582/1\*6WWJSfyH6nmODI2X7YpF4g.jpeg)

After — Look how the action parameter is empty

&#x20;                                           ![](https://miro.medium.com/max/593/1\*mW\_ZJm6ic50x-zBnXpkJAg.jpeg)

## Flag Capture <a href="#2178" id="2178"></a>

Click on the ‘Spin for question’ button and then right-click, to open the Inspect option

Let’s try putting the /flash fast/answer value back to the action parameter

Left-click to save the changes

On my screen, I have the values ‘45992’ and ‘30911’ and have the blue dot highlighted against the addition sign. This indicates that the addition operation must be performed

&#x20;                                                ![](https://miro.medium.com/max/782/1\*ukBLryv3h3J\_1L6OOl-hjw.jpeg)

The sum is 76903

Click to submit the answer and capture the flag!

> Flag — b3NqEDBNz3MksjSMVsVe

1800 points on the board.Onward to the next challenge!

&#x20;                                                   ![](https://miro.medium.com/max/525/1\*Hnfjo\_ezFFVeShOLwEneDw.jpeg)
