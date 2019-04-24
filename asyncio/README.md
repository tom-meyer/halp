### Main

    import asyncio

    async def app(loop):
        pass

    def main():
        loop = asyncio.get_event_loop()
        loop.run_until_complete(app(loop))

    if __name__ == '__main__':
        main()
