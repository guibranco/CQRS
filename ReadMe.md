# MediatR

CQRS with MediatR in .NET Core.

## Command

 ```csharp
public class InsertProductCommand : IRequest
{
    public string Description { get; set; }
}
 ```

## CommandHandler

```csharp
    public class InsertProductCommandHandler : AsyncRequestHandler<InsertProductCommand>
    {
        protected override Task Handle(InsertProductCommand request, CancellationToken cancellationToken)
        {
            /// Implementation
        }
    }
```

## Query

```csharp
public class GetProductByIdQuery : IRequest<ProductViewModel>
{
    public long Id { get; set; }
}
```

## QueryHandler

```csharp
public class GetProductByIdQueryHandler : IRequestHandler<GetProductByIdQuery, ProductViewModel>
{
    public Task<ProductViewModel> Handle(GetProductByIdQuery request, CancellationToken cancellationToken)
    {
        /// Implementation
    }
}
```

## Notification

```csharp
public class ProductInsertedNotification : INotification
{
    public long Id { get; set; }

    public string Description { get; set; }
}
```

## NotificationHandler

```csharp
public class ProductInsertedNotificationHandler : INotificationHandler<ProductInsertedNotification>
{
    public Task Handle(ProductInsertedNotification notification, CancellationToken cancellationToken)
    {
        /// Implementation
    }
}
```

## Tests

```csharp
[TestClass]
public class Tests
{
    public Tests()
    {
        var services = new ServiceCollection();
        services.AddMediatR(typeof(InsertProductCommand));
        Mediator = services.BuildServiceProvider().GetService<IMediator>();
    }

    private IMediator Mediator { get; }

    [TestMethod]
    public async Task DeleteProductCommand()
    {
        await Mediator.Send(new DeleteProductCommand { Id = 1 });

        await Mediator.Publish(new ProductDeletedNotification());
    }

    [TestMethod]
    public async Task GetProductByIdQuery()
    {
        var result = await Mediator.Send(new GetProductByIdQuery { Id = 1 });
    }

    [TestMethod]
    public async Task InsertProductCommand()
    {
        await Mediator.Send(new InsertProductCommand { Description = "Description" });

        await Mediator.Publish(new ProductInsertedNotification());
    }

    [TestMethod]
    public async Task UpdateProductCommand()
    {
        await Mediator.Send(new UpdateProductCommand { Id = 1, Description = "Description" });

        await Mediator.Publish(new ProductUpdatedNotification());
    }
}
```

## Feature Folders

**Category**

    Delete

        DeleteCategoryCommand.cs

        DeleteCategoryCommandResult.cs

        DeleteCategoryCommandValidator.cs

        DeleteCategoryCommandHandler.cs

    Insert

        InsertCategoryCommand.cs

        InsertCategoryCommandResult.cs

        InsertCategoryCommandValidator.cs

        InsertCategoryCommandHandler.cs

    List

        ListCategoryQuery.cs

        ListCategoryQueryResult.cs

        ListCategoryQueryValidator.cs

        ListCategoryQueryHandler.cs

    Update

        UpdateCategoryCommand.cs

        UpdateCategoryCommandResult.cs

        UpdateCategoryCommandValidator.cs

        UpdateCategoryCommandHandler.cs

**Product**

    Delete

        DeleteProductCommand.cs

        DeleteProductCommandResult.cs

        DeleteProductCommandValidator.cs

        DeleteProductCommandHandler.cs

    Insert

        InsertProductCommand.cs

        InsertProductCommandResult.cs

        InsertProductCommandValidator.cs

        InsertProductCommandHandler.cs

    List

        ListProductQuery.cs

        ListProductQueryResult.cs

        ListProductQueryValidator.cs

        ListProductQueryHandler.cs

    SelectById

        SelectByIdProductQuery.cs

        SelectByIdProductQueryResult.cs

        SelectByIdProductQueryValidator.cs

        SelectByIdProductQueryHandler.cs

    Update

        UpdateProductCommand.cs

        UpdateProductCommandResult.cs

        UpdateProductCommandValidator.cs

        UpdateProductCommandHandler.cs

    UpdateCategory

        UpdateCategoryProductCommand.cs

        UpdateCategoryProductCommandResult.cs

        UpdateCategoryProductCommandValidator.cs

        UpdateCategoryProductCommandHandler.cs

    UpdatePrice

        UpdatePriceProductCommand.cs

        UpdatePriceProductCommandResult.cs

        UpdatePriceProductCommandValidator.cs

        UpdatePriceProductCommandHandler.cs
