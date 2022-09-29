# Obj-C

//
//  main.m
//  ObjectiveCTest
//
//  Created by David on 2022/08/31.
//

#import <Foundation/Foundation.h>

static int ignorePacketBitTable[168];

@interface PacketProfiler : NSObject
{
    int packetInfo[168];
    char* name;
}

@end

@implementation PacketProfiler
+ (void)initialize
{
    NSLog(@"Hello, init");
}

-setName: (char *)nameStr
{
    name = nameStr;
    return self;
}

- (char *)namePrint
{
    return name;
}

- packetCount
{
    packetInfo[1]++;
    
    return self;
}

- (BOOL) checkThreashod
{
    return YES;
}

- countPacket
{
    packetInfo[1]++;
    return self;
}


@end

@interface Process : NSObject
{
    PacketProfiler *profiler;
}
+ run;

@end
@implementation Process
+ run
{
    while(1){
        NSLog(@"Hello, Thread2!");
    }
    return self;
     
}
- init
{
    
    PacketProfiler *profiler1  = [[PacketProfiler alloc] init];
    [profiler1 setName: "11"];
    PacketProfiler *profiler2  = [[PacketProfiler alloc] init];
    [profiler2 setName: "22"];
    NSThread* t1 = [[NSThread alloc]
                    initWithTarget:self selector:@selector(run:)
                                             object: profiler1];
    NSThread* t2 = [[NSThread alloc]
                    initWithTarget:self selector:@selector(run:)
                                             object: profiler2];
    [t1 start];
    [t2 start];

    return self;
}
- run: (id) profilerEachThread
{
    bool opt;
    
    while(1)
    {

        char *pName = [profilerEachThread namePrint];

        NSLog(@"%s  %@",pName, [NSThread currentThread]);
  
        [NSThread sleepForTimeInterval:1.0f];
    }
    return self;
     
}

@end
@interface Local : Process
- run;

@end
@implementation Local
- init
{
    PacketProfiler *profiler1  = [[PacketProfiler alloc] init];
    [profiler1 setName: "11"];
    PacketProfiler *profiler2  = [[PacketProfiler alloc] init];
    [profiler2 setName: "22"];
    NSThread* t1 = [[NSThread alloc]
                    initWithTarget:self selector:@selector(run:)
                                             object: profiler1];
    NSThread* t2 = [[NSThread alloc]
                    initWithTarget:self selector:@selector(run:)
                                             object: profiler2];
    [t1 start];
    [t2 start];
    return self;
}
- run:(id) profile
{
    bool opt;
    
    while(1)
    {
        //NSLog(@"%s  %@",pName, [NSThread currentThread]);
  
        [NSThread sleepForTimeInterval:1.0f];
        [super run: profile];
    }
    return self;
}
@end

int main(int argc, const char * argv[]) {

    id p1 = [[Local alloc] init];

    [NSThread sleepForTimeInterval:200.0f];
    id p3 = [[PacketProfiler alloc] init];
    id p2 = [[PacketProfiler alloc] init];
    return 0;
}
