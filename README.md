# THOP: PyTorch-OpCounter

## How to install 
* Through PyPi
    
    `pip install thop`
    
* Using GitHub (always latest)
    
    `pip install --upgrade git+https://github.com/JJBOY/pytorch-OpCounter.git`
    
## How to use 
* Basic usage 
    ```python
    from torchvision.models import resnet50
    from thop import profile
    model = resnet50()
    input = torch.randn(1, 3, 224, 224)
    flops, params = profile(model, inputs=(input, ))
    ```    

* Define the rule for 3rd party module.
    ```python
    class YourModule(nn.Module):
        # your definition
    def count_your_model(model, x, y):
        # your rule here
    
    input = torch.randn(1, 3, 224, 224)
    flops, params = profile(model, inputs=(input, ), 
                            custom_ops={YourModule: count_your_model})
    ```
    
* Improve the output readability

    Call `thop.clever_format` to give a better format of the output.
    ```python
    from thop import clever_format
    flops, params = clever_format([flops, params], "%.3f")
    ```    

