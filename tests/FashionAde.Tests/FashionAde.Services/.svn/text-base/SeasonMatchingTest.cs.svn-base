using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using NUnit.Framework;
using FashionAde.Core.Services;
using FashionAde.Core.Clothing;
using FashionAde.Core;
using FashionAde.Core.OutfitEngine;

namespace Tests.FashionAde.Services
{
    [TestFixture]
    public class SeasonMatchingTest
    {
        [Test]
        public void CanMatchSeasons()
        {
            HashSet<int> seasons = new HashSet<int>();
            HashSet<int> eventTypes = new HashSet<int>();
            PreOutfit po = new PreOutfit();

            Combination c = new Combination();
            c.GarmentA = new MasterGarment();
            c.GarmentA.EventCode = 1;
            c.GarmentA.SeasonCode = 1;

            po.Accesory1 = new MasterGarment();
            po.Accesory1.EventCode = 3;
            po.Accesory1.SeasonCode = 3;

            c.GarmentB = new MasterGarment();
            c.GarmentB.EventCode = 7;
            c.GarmentB.SeasonCode = 7;

            po.Combination = c;
            OutfitValidationService.VerifyAndSetSeasonsAndEventTypes(seasons, eventTypes, po);

            Assert.IsTrue(seasons.Sum() == 1);
            Assert.IsTrue(eventTypes.Sum() == 1);
        }
    }
}
