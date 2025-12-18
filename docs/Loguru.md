from loguru import logger

@logger.catch
def my_function(x, y):
    return x / y



my_function(10, 0)