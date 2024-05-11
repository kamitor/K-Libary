---
quickshare-date: 2023-03-20 10:23:41
quickshare-url: "https://noteshare.space/note/clfgmdics1282601pjie3ta8hy#7ZrWNH9kHh1ZqXs+gzUFBE89rI14EYp9eofLcVmveWs"
---
[[Beergame Central]]



# Testing objectives:
Stess test the application for multipule users and multipule games.
Stress test the application by making multipule requests at the same time.
Performance test: Test when the application slows down or otherwise fails to meet demands. 

Perform system testing: System testing is used to test the application as a whole. This can be done by creating test cases that test the application's functionality, performance, and compatibility with other systems.

Perform acceptance testing: Acceptance testing is used to verify that the application meets the needs of the users. This can be done by having actual users test the application and provide feedback.
 
Original request:

"Chris can you see if you can stress test the application"

# test environment:
The test evironment is online on http://demonstrator.sparklivinglab.nl/
The application might be taken to local in order to increase the testing possibilities. 

Test software;
After looking at the code, there are already some unit tests created in  https://github.com/Hogeschool-Windesheim/blockchain-demonstrator-serious-game/tree/main/BlockchainDemonstratorNUnitTest
these are written in Nunit.

As a preparation I have written some Nunit tests that could work for this code:
```
using NUnit.Framework;

namespace GameTests
{
    [TestFixture]
    public class GameCreationTests
    {
        [Test]
        public void CanCreateMultipleGamesWithFourPlayers()
        {
            // Arrange
            var gameService = new GameService();
            var player1 = new Player("Player 1");
            var player2 = new Player("Player 2");
            var player3 = new Player("Player 3");
            var player4 = new Player("Player 4");

            // Act
            var game1 = gameService.CreateGame(player1, player2, player3, player4);
            var game2 = gameService.CreateGame(player1, player2, player3, player4);

            // Assert
            Assert.IsNotNull(game1);
            Assert.IsNotNull(game2);
            Assert.AreEqual(4, game1.Players.Count);
            Assert.AreEqual(4, game2.Players.Count);
        }
    }
}

```

 The test creates four `Player` objects and then uses the `GameService` to create two games, each with the four players. It then asserts that both games were created successfully and that each game has four players.

``
```
using NUnit.Framework;

namespace GameTests
{
    [TestFixture]
    public class StressTests
    {
        [Test]
        public void CanHandleMultipleConcurrentOrders()
        {
            // Arrange
            var gameService = new GameService();
            var player1 = new Player("Player 1");
            var player2 = new Player("Player 2");
            var player3 = new Player("Player 3");
            var player4 = new Player("Player 4");
            var game1 = gameService.CreateGame(player1, player2, player3, player4);
            var game2 = gameService.CreateGame(player1, player2, player3, player4);
            var game3 = gameService.CreateGame(player1, player2, player3, player4);

            // Act
            var stopwatch = Stopwatch.StartNew();
            var orders = new List<Task>();
            for (int i = 0; i < 4; i++)
            {
                orders.Add(game1.Order("Item 1", 4));
                orders.Add(game2.Order("Item 1", 4));
                orders.Add(game3.Order("Item 1", 4));
            }

            Task.WaitAll(orders.ToArray());
            stopwatch.Stop();

            // Assert
            Assert.LessOrEqual(stopwatch.ElapsedMilliseconds, 3000); //3 seconds allowed
        }
    }
}

```

the stress test creates a `GameService` object, four `Player` objects and 3 games, each with 4 players. Then it uses a `Stopwatch` to measure the time it takes to complete 12 orders (3 games * 4 players = 12 orders) of "Item 1" with a quantity of 4. The test then asserts that the time taken is less than or equal to 3 seconds.


# Dealing with the annoying issues;
It strook me that it might be possible to just direct the host file in order to solve this problem as a shortcut; 

1.  Open the hosts file: The location of the hosts file depends on your operating system. On Windows, it is located at `C:\Windows\System32\drivers\etc\hosts`. On Mac and Linux, it is located at `/etc/hosts`. You will need to open the file as an administrator to make changes.
    
2.  Add a new line to the file: Add a new line to the file with the following format: `127.0.0.1 http://demonstrator.sparklivinglab.nl.  

2.  Add a new line to the file: Add a new line to the file with the following format: `127.0.0.1 https://demonstrator.sparklivinglab.nl.  


4.  Verify the change: Once you've saved the file, you can test the change by opening a web browser and navigating to the domain you just added. It should redirect to your localhost.